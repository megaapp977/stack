# WaVoIP Webhook Configuration for Recordings

## Description

This guide explains how to configure WaVoIP webhooks to receive automatic notifications when call recordings are ready for download.

## Why it's necessary

WaVoIP processes recordings asynchronously. After a call ends, the recording goes through several states:

- `RECORDING` - Recording in progress
- `MIXING` - Processing/mixing audio
- `READY` - Recording ready for download!
- `DISABLED` - Recordings disabled
- `EMPTY_RECORDING` - Very short call, no recording

Without the webhook configured, the system does polling (increasingly spaced retries) waiting for the recording to be ready, which can fail if it takes too long.

**With the webhook configured**, WaVoIP automatically notifies when the recording is ready, and it's downloaded immediately.

## Configuration

### 1. Get the Webhook URL

Your webhook URL is:

```
https://YOUR-DOMAIN.com/webhooks/wavoip
```

For example:

- Production: `https://app.yourcompany.com/webhooks/wavoip`
- Development: `https://staging.yourcompany.com/webhooks/wavoip`

### 2. Configure in WaVoIP

1. Access the WaVoIP panel: <https://app.wavoip.com/devices>
2. Select the device you want to configure
3. In the side menu, go to **Integrations > Webhook**
4. Enter the webhook URL (from step 1)
5. Click **Save**
6. **Important**: Enable the `RECORD` event

### 3. Verify the configuration

After configuring, make a short test call. You should see in the logs:

```
[WaVoIP Webhook] Received event: RECORD
[WaVoIP Webhook] Recording READY for call 123456
[WaVoIP Recording Webhook] ✅ Recording attached successfully
```

## Webhook Format

WaVoIP sends webhooks with these events:

### RECORD Event

```json
{
    "type": "RECORD",
    "action": "UPDATE",
    "whatsapp_call_id": 123456,
    "id_session": 789,
    "record_status": "READY",
    "record_url": "https://storage.wavoip.com/123456"
}
```

### CALL Event

```json
{
    "type": "CALL",
    "action": "CREATE",
    "whatsapp_call_id": 123456,
    "status": "ACTIVE",
    "direction": "INCOMING",
    "duration": 45,
    "record_status": "RECORDING"
}
```

## Troubleshooting

### Recordings are not downloaded

1. **Verify the webhook URL** - Make sure it's publicly accessible
2. **Check the logs** - Look for `[WaVoIP Webhook]` to see if events are arriving
3. **Test manually** - Make a test POST request:

   ```bash
   curl -X POST https://your-domain.com/webhooks/wavoip \
     -H "Content-Type: application/json" \
     -d '{"type":"RECORD","whatsapp_call_id":"test123","record_status":"READY"}'
   ```

### The webhook doesn't arrive

1. Verify that the device has the webhook enabled in WaVoIP
2. Confirm that the `RECORD` event is selected
3. Check if there are firewalls blocking requests from WaVoIP

### The recording is downloaded but is empty

This can occur if the call was very short. WaVoIP sends `record_status: "EMPTY_RECORDING"` for these calls.

## Backup system (Polling)

If the webhook is not configured or fails, the system automatically:

1. Attempts to download the recording with exponential retries
2. Waits up to 4 hours with increasingly spaced retries
3. Marks the message as "failed" if it can't download after all attempts

**Recommendation**: Always configure the webhook for greater reliability.

## References

- [Official WaVoIP Documentation - Recording](https://wavoip.gitbook.io/api/gravacao)
- [Official WaVoIP Documentation - Webhook](https://wavoip.gitbook.io/api/webhook-beta)
