# Database Index Migrations Guide for Production

## Problem

When creating indexes on large tables (>10M records) in production, lock timeouts may occur that prevent the migration from completing.

## Large tables in this project

- `messages` - >50M records
- `conversations` - >10M records  
- `contacts` - >5M records
- `notifications` - >20M records

## Best practices

### 1. Always use concurrent indexes

```ruby
class AddMyIndex < ActiveRecord::Migration[7.1]
  disable_ddl_transaction!  # ← REQUIRED for concurrent
  
  def change
    add_index :table, :column, 
      algorithm: :concurrently,  # ← Doesn't block writes
      if_not_exists: true        # ← Idempotent
  end
end
```

### 2. Split large migrations

❌ **Bad**: 20 indexes in one migration
```ruby
def change
  add_index :table1, :col1, algorithm: :concurrently
  add_index :table2, :col2, algorithm: :concurrently
  # ... 18 more
end
```

✅ **Good**: One migration per large table
```ruby
# 20241230_add_messages_indexes.rb
def change
  add_index :messages, :source_id, algorithm: :concurrently
end

# 20241230_add_conversations_indexes.rb  
def change
  add_index :conversations, [:account_id, :status], algorithm: :concurrently
end
```

### 3. Configure timeouts in migrations

```ruby
class AddIndexToLargeTable < ActiveRecord::Migration[7.1]
  disable_ddl_transaction!
  
  def up
    # Only in production
    if Rails.env.production?
      execute('SET statement_timeout = "30min"')
      execute('SET lock_timeout = "5min"')
    end
    
    add_index :large_table, :column, algorithm: :concurrently
  end
end
```

### 4. Use partial indexes when possible

```ruby
# ❌ Bad: index entire table
add_index :conversations, :status

# ✅ Good: only active records (10% of total)
add_index :conversations, :status,
  where: 'status IN (0, 1) AND deleted_at IS NULL',
  name: 'idx_conversations_active'
```

### 5. Monitor index creation

```bash
# View progress in real-time
bundle exec rails db:indexes:monitor

# Direct SQL query
SELECT 
  phase, 
  round(100.0 * blocks_done / nullif(blocks_total, 0), 1) as percent,
  age(now(), query_start) as duration
FROM pg_stat_progress_create_index p
JOIN pg_stat_activity a ON p.pid = a.pid;
```

## Recommended workflow

### For development/staging
```bash
bundle exec rails db:migrate
```

### For production - indexes on large tables

1. **Review migration before deploying**
   ```bash
   # View pending migrations
   bundle exec rails db:migrate:status
   
   # Check missing indexes
   bundle exec rails db:indexes:check_missing
   ```

2. **Option A: Execute during maintenance window**
   ```bash
   # Stop workers
   docker-compose stop worker
   
   # Run migration
   bundle exec rails db:migrate
   
   # Restart workers
   docker-compose start worker
   ```

3. **Option B: Execute during low activity hours (early morning)**
   ```bash
   # Use safe rake task
   bundle exec rails db:indexes:create_pending
   
   # Or manually:
   bundle exec rails runner "
     execute('SET statement_timeout = \"30min\"')
     execute('SET lock_timeout = \"5min\"')
     add_index :table, :column, algorithm: :concurrently
   "
   ```

4. **Option C: Skip temporarily**
   ```bash
   # Mark as executed
   bundle exec rails runner "
     ActiveRecord::Base.connection.execute(
       \\\"INSERT INTO schema_migrations (version) 
        VALUES ('YYYYMMDDHHMMSS') ON CONFLICT DO NOTHING\\\"
     )
   "
   
   # Create index later manually
   bundle exec rails db:indexes:create_pending
   ```

## Troubleshooting

### Error: `PG::LockNotAvailable: lock timeout`
**Cause**: Could not acquire lock within timeout
**Solution**: Execute during lower activity hours

### Error: `PG::QueryCanceled: statement timeout`  
**Cause**: Index took too long to create
**Solution**: Increase `statement_timeout` or use partial index

### View blocked queries
```sql
SELECT 
  pid,
  usename,
  pg_blocking_pids(pid) as blocked_by,
  query as blocked_query
FROM pg_stat_activity
WHERE cardinality(pg_blocking_pids(pid)) > 0;
```

### Cancel index creation
```sql
-- View PIDs of indexes being created
SELECT pid FROM pg_stat_progress_create_index;

-- Cancel (if safe)
SELECT pg_cancel_backend(pid);
```

## Checklist before deploy

- [ ] Does migration create indexes on large tables?
- [ ] Uses `disable_ddl_transaction!`?
- [ ] Uses `algorithm: :concurrently`?
- [ ] Uses `if_not_exists: true`?
- [ ] Configures timeouts for production?
- [ ] Split into small migrations?
- [ ] Coordinated low activity schedule if necessary?

## Useful tools

```bash
# Check missing indexes
bundle exec rails db:indexes:check_missing

# Create pending indexes (early morning)
bundle exec rails db:indexes:create_pending

# Automatic creation (for cron)
bundle exec rails db:indexes:auto_create

# Monitor progress
bundle exec rails db:indexes:monitor

# View migration status
bundle exec rails db:migrate:status
```

## Cron Configuration (automation)

Chatwoot uses **sidekiq-cron** for scheduled tasks. Automatic index creation is already configured in `config/schedule.yml`.

### Automatic configuration

The `Internal::CreatePendingIndexesJob` runs daily at 2:30 AM UTC:

```yaml
# config/schedule.yml
create_pending_indexes_job:
  cron: '30 2 * * *'
  class: 'Internal::CreatePendingIndexesJob'
  queue: low
  active_job: true
```

### Environment variables (optional)

```bash
# config/application.yml or .env
INDEX_SAFE_HOURS=2-5                      # Safe hours (2:00-5:00 AM)
INDEX_MAX_DURATION_MINUTES=120            # Maximum 2 hours per execution
INDEX_MAX_ACTIVE_CONNECTIONS=50           # Cancel if system is too busy
```

### Automatic behavior

The job automatically:
- ✅ Only runs in production/staging
- ✅ Verifies it's within safe hours (2-5 AM by default)
- ✅ Cancels if system load is too high
- ✅ Limits maximum duration (2 hours by default)
- ✅ Stops if outside safe hours
- ✅ Logs everything to Sidekiq logs

### Monitor executions

```bash
# View Sidekiq logs
tail -f log/sidekiq.log | grep CreatePendingIndexesJob

# View in Sidekiq Web UI
# http://your-app.com/sidekiq/cron

# Execute manually from Rails console
Internal::CreatePendingIndexesJob.perform_now

# Or from rake
bundle exec rails db:indexes:auto_create
```

## References

- [PostgreSQL: Building Indexes Concurrently](https://www.postgresql.org/docs/current/sql-createindex.html#SQL-CREATEINDEX-CONCURRENTLY)
- [Rails: Safe Migrations](https://github.com/ankane/strong_migrations)
