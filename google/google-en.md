# Self-hosted MEGA: Google integration

Consolidated documentation for MEGA's Google options: Gmail/Google Workspace, OAuth sign-in, Google Cloud Platform (GCP) deployment, and Google Cloud Storage (GCS).

## Google Workspace and Gmail with OAuth

Less-secure Google Workspace apps are no longer an option for this integration. To let MEGA read and manage Gmail or Google Workspace mail, create an OAuth app in Google Cloud.

### APIs to enable for each use

Open **APIs & Services > Library**, find the service, and select **Enable**. Enable only the services that apply:

| MEGA function | API to enable | Required? |
|---|---|---|
| Google Calendar synchronization | **Google Calendar API** | Yes |
| Attachments in a GCS bucket | **Cloud Storage API** | Yes |
| Gmail/Google Workspace over OAuth IMAP and SMTP | No extra REST API | Do not enable Gmail API for this flow alone |
| Google sign-in | No extra REST API | No additional API is required |
| Future Gmail REST calls | **Gmail API** | Only if MEGA starts calling Gmail API endpoints |

MEGA uses OAuth XOAUTH2 with `imap.gmail.com` and `smtp.gmail.com` for mail. It therefore needs the `https://mail.google.com/` scope, but not Gmail API. APIs are enabled in **Library**; permissions a user grants are separately declared in **Google Auth Platform > Data Access**.

1. In the [Google API Console](https://console.developers.google.com/), create or select the project and register the OAuth app.
2. For the email-channel app, add `https://<your-instance-url>/google/callback` as an authorized redirect URL.
3. Copy the client ID and secret to MEGA:

```bash
GOOGLE_OAUTH_CLIENT_ID=369777777777-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.apps.googleusercontent.com
GOOGLE_OAUTH_CLIENT_SECRET=ABCDEF-GHijklmnoPqrstuvwX-yz1234567
```

![OAuth app registration](images/oauth-app-setup.png)

If an app already exists for Google OAuth sign-in, reuse it by adding this redirect URL; do not remove the existing one. Restart MEGA after changing the variables.

### Required OAuth scopes

In **OAuth consent screen** > **Edit App**, add and save:

- `https://mail.google.com/`: read, send, delete, and manage email.
- `email`: view the user's email address.
- `profile`: view the user's name, picture, and basic profile data.

![Adding the mail scope](images/add-scope-demo.gif)

Organizations with fewer than 100 users can keep the app in testing mode. To serve more than 100 users or multiple clients, publish it. Because it uses a restricted scope, complete Google's [verification process](https://support.google.com/cloud/answer/9110914), which can take several days.

## Google sign-in

Sign-in OAuth uses a different callback from the Gmail channel. Set all three variables and restart MEGA:

```bash
GOOGLE_OAUTH_CLIENT_ID=369777777777-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.apps.googleusercontent.com
GOOGLE_OAUTH_CLIENT_SECRET=ABCDEF-GHijklmnoPqrstuvwX-yz1234567
GOOGLE_OAUTH_CALLBACK_URL=https://<your-server-domain>/omniauth/google_oauth2/callback
```

The `/omniauth/google_oauth2/callback` path is fixed in MEGA and must exactly match the authorized URL in Google API Console.

## Google Calendar in MEGA

MEGA uses the same global OAuth credentials for Google Calendar and, optionally, Google sign-in. Configure the credential once per installation; then each account connects its own calendar from **Settings > Integrations > Google Calendar**.

### Google Cloud setup

1. In **APIs & Services > Library**, enable **Google Calendar API**.
2. In **OAuth consent screen**, complete the app details. Use **Internal** only for users in the same Google Workspace; use **External** for customer Gmail or Workspace accounts. Add test users while the app remains in testing.
3. Add the scopes requested by MEGA:

```text
openid
email
profile
https://www.googleapis.com/auth/calendar
```

4. In **APIs & Services > Credentials**, create a **Web application** OAuth client.
5. Under *Authorized JavaScript origins*, add only the HTTPS origin—no path or trailing `/`: `https://<your-domain>`.
6. Under *Authorized redirect URIs*, add the required Calendar callback:

```text
https://<your-domain>/google_calendar/callback
```

If Google sign-in is also enabled, add:

```text
https://<your-domain>/omniauth/google_oauth2/callback
```

> Calendar and sign-in use different URLs. In MEGA, the Calendar URL is built from `FRONTEND_URL` plus `/google_calendar/callback`; the public domain in `FRONTEND_URL` must therefore exactly match the authorized origin and callback.

### Add credentials from Super Admin

As a super admin, open:

```text
https://<your-domain>/super_admin/app_config?config=google
```

![Google configuration in Super Admin](images/super-admin-google-settings.png)

Complete and save the fields displayed in **Configure Settings - Google**:

| Field | Value |
|---|---|
| Google OAuth Client ID | Client ID from Google Cloud |
| Google OAuth Client Secret | Client Secret from Google Cloud |
| Google OAuth Redirect URI | `https://<your-domain>/google_calendar/callback` |
| Enable Google OAuth login | `False` for Calendar only; `True` to also allow Google sign-in |

When credentials are entered in Super Admin, you do not need to store the Client ID or secret in environment variables. Keep `FRONTEND_URL=https://<your-domain>` on the server. Environment variables remain a valid fallback for legacy deployments.

### Connect a calendar per account

1. In the relevant account, open **Settings > Integrations > Google Calendar**.
2. Select **Connect**, choose the Google account, and grant the requested permissions.
3. Back in MEGA, select or confirm the destination calendar and save the settings.
4. Enable synchronization, select its direction (**MEGA → Google**, **Google → MEGA**, or **Bidirectional**), and enable the required modules: Calendar, Kanban, Conversations, and Reminders.

The Google Calendar card is available only when the account feature is enabled and global Client ID and Client Secret values exist. The connection and tokens are stored per account, not as an installation-wide shared calendar.

## Deploy MEGA on GCP

This guide uses one Compute Engine VM for MEGA. For cloud-native deployment, use Helm charts with Google Kubernetes Engine (GKE).

1. In GCP, open **VM > Compute Engine** and create an instance.
2. Choose the correct region, at least 4 vCPUs and 8 GB RAM (N2 general-purpose).
3. Choose Ubuntu 20.04 with a 120 GB disk.
4. SSH into it and follow the MEGA Linux VM installation.
5. Open `http://<your-instance-ip>:3000`, or `https://<your-domain>` once domain setup is complete.

![Compute Engine VM creation](images/gcp-compute-engine.png)

Then set the domain, email, and other environment variables for the Linux VM installation.

## Store attachments in Google Cloud Storage

Before creating or using the bucket, enable **Cloud Storage API** in **APIs & Services > Library**.

Enable GCS as the storage service:

```bash
ACTIVE_STORAGE_SERVICE='google'
```

### Project and bucket

1. Copy the project ID from Google Cloud Console:

```bash
GCS_PROJECT=your-project-id
```

![Project ID location](images/get-project-id.png)

2. Go to **Storage > Browser**, use **Create bucket**, and keep the default choices when they suit your environment.

![Bucket creation](images/create-bucket.png)

3. Set the resulting bucket name:

```bash
GCS_BUCKET=your-bucket-name
```

### Service account and credentials

1. Go to **Identity & Services > Identity > Service Accounts**, create a service account, and grant **Cloud Storage > Storage Admin**.

![Storage Admin role](images/storage-admin.png)

2. In **Storage > Browser > your bucket > Permissions**, add that service account as a member with **Cloud Storage > Storage Admin**.

![Bucket permissions](images/bucket-permissions.png)

3. In the service account, select **Keys > Add Key** and choose JSON.

![JSON key creation](images/service-account-json-key.png)

Paste the JSON content on one line. In MEGA 2.17+, wrap the value in single quotes:

```bash
GCS_CREDENTIALS='{"type":"service_account","project_id":"","private_key_id":"","private_key":"","client_email":"","client_id":"","auth_uri":"","token_uri":"","auth_provider_x509_cert_url":"","client_x509_cert_url":""}'
```

### Direct upload

Attachments normally pass through the MEGA server first. To upload directly to GCS, enable:

```bash
DIRECT_UPLOADS_ENABLED=true
```

Then configure [bucket CORS](https://edgeguides.rubyonrails.org/active_storage_overview.html#cross-origin-resource-sharing-cors-configuration) to allow direct uploads.
