# Setting Up the WooCommerce Integration in MEGA

Connect your WooCommerce store to MEGA to see each customer's orders right inside the conversation.

Once the integration is active, agents see the contact's recent orders in the conversation sidebar: order number, status, date, and total. Each order number opens the order in the WordPress admin. Optionally, MEGA can also post a note in the conversation whenever an order's status changes.

Setup takes **3 steps** (the third one is optional).

## Prerequisites

Before you start, make sure you have:

1. **A WooCommerce store published over HTTPS** and reachable from the internet (MEGA queries the store from its servers, not from your browser)
2. **Pretty permalinks enabled** in WordPress: under **Settings → Permalinks**, any option other than **Plain** must be selected. Without it, the WooCommerce API (`/wp-json/...`) does not respond
3. **Administrator access** to WordPress / WooCommerce
4. **Administrator access** to your MEGA account
5. **The WooCommerce integration enabled on your plan**

> **📌 Note:** WooCommerce is a premium feature. If you don't see the **WooCommerce** card under **Settings → Integrations**, your plan doesn't include it yet. Ask your MEGA provider to enable it for your account.

## Step 1 — Create the API keys in WooCommerce

1. In WordPress, go to **WooCommerce → Settings → Advanced → REST API**
2. Click **Add key**
3. Fill in the fields:
   - **Description**: e.g. "MEGA"
   - **User**: an administrator or shop manager user
   - **Permissions**: **Read**
4. Click **Generate API key**
5. Copy and store somewhere safe:
   - **Consumer key**, starts with `ck_`
   - **Consumer secret**, starts with `cs_`

> **⚠️ Important**
> WooCommerce shows the consumer secret **only once**. If you lose it, revoke the key and generate a new one.

> **🔒 Security:** MEGA only reads orders and never changes them. **Read** permission is enough; do not grant **Read/Write**.

## Step 2 — Connect the store in MEGA

1. In MEGA, go to **Settings → Integrations**
2. Find **WooCommerce** and click **Connect**
3. Fill in the form:
   - **Store URL**: your store address, e.g. `https://www.mystore.com`
   - **Consumer Key**: the `ck_...` key from Step 1
   - **Consumer Secret**: the `cs_...` key from Step 1
4. Save

### How to enter the Store URL

- Use **exactly** the **Site Address (URL)** shown in WordPress under **Settings → General**
- Keep `https://` and `www` exactly as they appear there: `https://mystore.com` and `https://www.mystore.com` count as different stores
- Don't add `/wp-admin`, `/shop`, or other paths. A trailing slash doesn't matter
- If WordPress is installed in a subfolder (e.g. `https://mystore.com/shop`), include the subfolder

> **📌 Note:** MEGA doesn't test the keys when you save. The way to check that everything works is to open a conversation (see below).

### Check the connection

1. Open a conversation with a customer who has already bought from the store
2. In the right sidebar, expand the **WooCommerce Orders** section
3. You should see their recent orders, each with:
   - **Order #** (click it to open the order in WordPress)
   - **Status**: Pending, Processing, On hold, Completed, Cancelled, Refunded, or Failed
   - **Date** and **total** with its currency

### How MEGA finds a contact's orders

- MEGA searches orders by the contact's **email**. If the contact has no email, it searches by **phone**
- The contact's email must match the order's billing email. If the customer bought with a different email, their orders won't show up
- Phone search is less reliable: WooCommerce stores the phone exactly as the customer typed it, which may not match the international format MEGA uses (e.g. `+5491112345678`). Whenever possible, fill in the contact's email
- The **10 most recent orders** are shown
- If the contact has neither email nor phone, the section shows **No orders found**

> **💡 Tip:** You can reorder or collapse the **WooCommerce Orders** section in the sidebar, like any other section.

## Step 3 — Status change notes (optional)

With this step, every time an order's status changes, MEGA adds a note to the customer's conversation, for example:

> Order 1234 status updated to completed

The status appears exactly as WooCommerce sends it (`pending`, `processing`, `on-hold`, `completed`, `cancelled`, `refunded`, `failed`).

### Create the webhook in WooCommerce

1. In WordPress, go to **WooCommerce → Settings → Advanced → Webhooks**
2. Click **Add webhook**
3. Fill in the fields:
   - **Name**: e.g. "MEGA - orders"
   - **Status**: **Active**
   - **Topic**: **Order updated**
   - **Delivery URL**: `https://YOUR-MEGA-DOMAIN/woocommerce/callback` (replace `YOUR-MEGA-DOMAIN` with the address you use to open MEGA, e.g. `https://app.mycompany.com/woocommerce/callback`)
   - **Secret**: you can keep the value WooCommerce suggests
   - **API Version**: **WP REST API Integration v3**
4. Click **Save webhook**

> **💡 Tip:** If you also want a note when an order is created, repeat these steps with the **Order created** topic.

### How the notes work

- MEGA identifies the store by its address, which is why the **Store URL** from Step 2 must match the site address in WordPress
- The customer is matched by the order's **billing email** and, if there's no match, by the **billing phone**
- The note is added to the customer's **most recent conversation**. If the customer has no conversation in MEGA, nothing is added
- The **WooCommerce Orders** section loads when you open the conversation. If it's already open when the note arrives, reopen it to see the new status

## Troubleshooting

| Problem | Likely cause | Fix |
|---|---|---|
| **WooCommerce** doesn't appear under **Settings → Integrations** | Your plan doesn't include the integration | Ask your MEGA provider to enable it |
| The **WooCommerce Orders** section doesn't appear in the conversation | The integration isn't connected, or the section is hidden | Check Step 2 and the sidebar sections |
| The section shows an error loading orders | Wrong or revoked keys, mistyped Store URL, permalinks set to **Plain**, or a firewall / security plugin blocking `/wp-json/` | Check the keys and Store URL; enable permalinks; allow access to `/wp-json/wc/v3/` in your firewall, Cloudflare, or security plugin |
| **No orders found** for a customer who did buy | The contact's email doesn't match the billing email, or the contact has no email | Fix or add the contact's email |
| Status change notes don't arrive | Webhook inactive, wrong delivery URL, Store URL different from the site address, or the customer has no conversation in MEGA | Check Step 3. Under **WooCommerce → Status → Logs**, look for the `webhooks-delivery` logs to see the responses |
| The webhook shows as **Disabled** | WooCommerce disables it on its own after several failed deliveries | Fix the delivery URL and set it back to **Active** |

## Disconnecting the integration

1. In MEGA, go to **Settings → Integrations → WooCommerce** and delete the integration
2. In WordPress, go to **WooCommerce → Settings → Advanced → REST API** and **revoke** the key created for MEGA
3. If you created webhooks, delete them under **WooCommerce → Settings → Advanced → Webhooks**
