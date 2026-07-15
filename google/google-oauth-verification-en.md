# OAuth consent screen verification for MEGA

Preparation and submission guide for verifying MEGA with Google so it can use Google Calendar with external production accounts.

## Scope of this verification

MEGA requests these scopes to connect Google Calendar:

```text
openid
email
profile
https://www.googleapis.com/auth/calendar
```

Full Calendar access is a **sensitive** scope. A published external app needs brand and data-access verification before general users can authorize it. It is not a restricted scope; an annual security assessment applies if restricted scopes are added or their data is accessed from a third-party server.

Verification is generally not needed for development/testing only, limited personal use, or an **Internal** app used solely by the same Google Workspace organization. For customer Gmail or Workspace accounts, use **External** and prepare verification.

### Required APIs and OAuth relationship

In **APIs & Services > Library**, enable **Google Calendar API**: it is the API required for this verification and Calendar synchronization. OAuth verification is not completed merely by enabling an API; you must also declare the scopes in **Data Access** and demonstrate their use.

If the same installation uses other Google functions, enable **Cloud Storage API** for GCS. Do not enable **Gmail API** just because MEGA uses Gmail over OAuth: the current implementation uses IMAP/SMTP with XOAUTH2 and the `https://mail.google.com/` scope, not Gmail REST endpoints. Gmail API is required only if MEGA later adds Gmail REST calls.

## Before you start

Use a dedicated Google Cloud production project. Keep a separate project and OAuth client for development or staging. Gather:

- A public HTTPS domain you own: `https://<your-domain>`.
- A public home page that identifies MEGA, explains the Google Calendar integration, and is not only a login page.
- A public privacy policy on the same domain, also linked from the home page.
- Public terms of service on the same domain.
- Actively monitored support and developer-contact emails.
- A square MEGA logo representing the app, in PNG/JPG/BMP, no larger than 1 MB; 120 × 120 px is recommended.
- A Google account that is a project Owner or Editor and a verified owner of the domain in Google Search Console.
- An unlisted demonstration video and test credentials if a reviewer needs them.

The privacy policy must clearly state that MEGA requests Calendar permission so a user can connect their account, reads/creates/updates events according to configured synchronization, stores encrypted per-account tokens to maintain the connection, and lets users disconnect. It must describe all storage, use, or sharing of Google data and match the actual product behavior.

## 1. Verify the domain

1. In [Google Search Console](https://search.google.com/search-console), add and verify the root-domain property, for example `chat2one.com`.
2. Use that same Google account as an Owner or Editor of the Google Cloud project.
3. In Google Cloud Console, open **Google Auth Platform > Branding**. Under **Authorized domains**, add the root domain before registering its URLs.
4. Confirm that every domain used by the home page, policy, terms, authorized JavaScript origins, and redirect URIs is authorized and verified.

Do not use a third-party domain or a different-domain privacy policy.

## 2. Prepare Branding

In the current console, open **APIs & Services > OAuth consent screen**; it opens **Google Auth Platform**. Complete **Branding**:

| Field | MEGA preparation |
|---|---|
| App name | `MEGA` (must match the website, video, and product) |
| User support email | Real, monitored authorization-support inbox |
| App logo | MEGA-owned logo; do not use Google marks or logos |
| Application home page | Public MEGA home-page URL |
| Application privacy policy link | Public MEGA privacy-policy URL |
| Application terms of service link | Public MEGA terms URL |
| Developer contact information | One or more emails that will answer Google |

For an **External** production app, home page, privacy policy, and terms are required. The home page must link to the exact privacy policy listed in Branding. Do not change name, logo, or URLs while review is active.

## 3. Configure Audience, client, and data access

1. Under **Audience**, select **External** for customer users. Keep **Testing** while validating with test users; before production submission, move to **In production** when the console requires it.

![Audience: external app in testing with test users](images/google-auth-platform-audience.png)

2. Under **Clients**, create or review a **Web application** OAuth client. Add:

   ```text
   Authorized JavaScript origin: https://<your-domain>
   Authorized redirect URI: https://<your-domain>/google_calendar/callback
   ```

   When MEGA also enables Google sign-in, add `https://<your-domain>/omniauth/google_oauth2/callback`.

3. Under **Data Access**, declare only `openid`, `email`, `profile`, and `https://www.googleapis.com/auth/calendar`.
4. Enable **Google Calendar API** under **APIs & Services > Library**.
5. Verify in MEGA that a calendar connects, can be selected, syncs only enabled functions, and can be disconnected.

Do not add scopes “just in case.” If a feature reads only events, first evaluate a narrower scope; retain full Calendar access only when MEGA's read, create, update, or delete behavior requires it.

## 4. Prepare the submission

Before selecting **Submit for verification**, prepare a short, specific statement for each scope:

| Scope | MEGA justification |
|---|---|
| `openid`, `email`, `profile` | Identify the Google account authorized by the administrator and show the connected identity in the integration. |
| `https://www.googleapis.com/auth/calendar` | Let an administrator connect a calendar, select a destination, and synchronize MEGA events in the configured direction. |

Provide up to three MEGA feature-documentation links if the console asks. Describe only functionality that is already available to users—do not promise future work.

### Required demonstration video

Upload an **Unlisted** YouTube video. Do not show secrets, customer data, or real calendars. The video must be in English and show the end-to-end flow:

1. The public MEGA site with the same name, logo, and domain submitted for review.
2. Sign in as an administrator of a test account.
3. **Settings > Integrations > Google Calendar** and **Connect**.
4. The complete OAuth consent flow in English, including the browser address bar with the client ID and the requested scopes.
5. Selecting the test Google account and calendar.
6. Choosing synchronization direction/modules.
7. A real Calendar function: create or update an event from MEGA and show the result in the authorized calendar; if import is requested, also show reading events.
8. Disconnecting, or where a user can revoke the connection.

Do not hide the consent screen or replace the flow with still images; Google must see that shown scopes match declared scopes.

## 5. Submit and publish

1. In **Branding**, complete brand verification if **Verify Branding** appears. Once it reaches **Ready to publish**, click **Publish branding** within seven days.
2. Open **Verification Center**. You can request **Data access** verification only after branding is published.
3. Review scopes, paste the unlisted video link, and provide justifications and requested documentation.
4. Confirm policy compliance and select **Submit**.
5. Monitor the support email, developer-contact email, and Verification Center. Reply accurately to Google and avoid configuration changes while review is underway.

For planning, Google typically lists 2–3 business days for branding and up to 10 business days for sensitive scopes; these are not guaranteed. A sensitive-scope rejection can prevent new authorizations for those scopes until the request is corrected and resubmitted.

## Final checklist

- [ ] Production project separate from test project.
- [ ] Google Calendar API enabled.
- [ ] External audience and correct publishing state.
- [ ] Owned domain verified in Search Console by a project Owner/Editor.
- [ ] All authorized domains, origins, and callbacks match exactly.
- [ ] Public, consistent home page, privacy policy, and terms on the owned domain.
- [ ] Consistent MEGA branding in console, website, product, and video.
- [ ] Only minimum scopes declared; Calendar scope justified by visible features.
- [ ] Unlisted English video with full OAuth consent and real product flow.
- [ ] No secrets, tokens, or customer data in video or documentation.
- [ ] Active support and developer contacts ready to answer Google.

## Google references

- [Verification requirements](https://support.google.com/cloud/answer/13464321)
- [Sensitive scope verification](https://developers.google.com/identity/protocols/oauth2/production-readiness/sensitive-scope-verification)
- [Manage OAuth App Branding](https://support.google.com/cloud/answer/15549049)
- [OAuth verification FAQ](https://support.google.com/cloud/answer/13463817)
