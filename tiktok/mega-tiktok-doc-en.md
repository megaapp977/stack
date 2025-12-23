# TikTok Channel Creation in MEGA

## Step 1 — TikTok Business Account
You must have a **TikTok Business Account**. Personal accounts are not supported.

## Step 2 — Request Special Permissions
Access to the **TikTok Business Messaging API** requires manual approval.

1. Open the official documentation:
   https://business-api.tiktok.com/portal/docs?id=1832183871604753
2. Request access to *Business Messaging API*.
3. Provide:
   - Use case (support, customer service, etc.).
   - Platform: MEGA.
4. Wait for TikTok approval.

## Step 3 — Create TikTok Developer App
1. Create an app in TikTok Developers.
2. Obtain:
   - App ID
   - App Secret
3. Configure:
   - Redirect URL: `https://<FRONTEND_URL>/tiktok/callback`
   - Webhook URL: `https://<FRONTEND_URL>/webhooks/tiktok`

## Step 4 — Configure MEGA
1. Set environment variables:
   - `TIKTOK_APP_ID`
   - `TIKTOK_APP_SECRET`
2. Enable TikTok integration in admin settings.

## Step 5 — Authorize Account
1. Start the connection from MEGA.
2. You will be redirected to TikTok.
3. Approve the requested permissions.

## Step 6 — Automatic Channel Creation
After authorization:
- MEGA validates access.
- TikTok channel is created or updated.
- Associated inbox is enabled.

## Step 7 — Message Reception
TikTok sends events to the configured webhook.
Incoming messages appear automatically in MEGA.

## Limitations
- Business accounts only.
- User-initiated messages only.
- Supported types: text, image, shared post.
- Regional restrictions may apply.
