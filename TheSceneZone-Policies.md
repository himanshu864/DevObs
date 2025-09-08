## Launch Policies

> Company / legal

- [ ] Publishable **Privacy Policy**, **Terms of Use**, and **Refunds/Cancellations** (esp. for tickets).
- [ ] Implement **in-app account deletion** and a **web URL** for account/data deletion.
- [ ] Ensure compliance with India’s **DPDP Act 2023** (data protection contact)

> Payments and Tickets

- [ ] Use third-party payments (Stripe/Razorpay) that includes apple pay
- [ ] If you pay out artists/venues, use a **marketplace processor** (e.g., **Stripe Connect**) to handle KYC/AML, payouts, and tax forms. Don’t build this yourself.

> User-generated Content (UGC) photos upload

- [ ] Add **report/block**, **moderation**, **content filters**, and an **EULA / house rules** (no abuse/illegal content).

> Privacy and Data

- [ ] Fill Apple’s **App Privacy** (privacy “nutrition labels”) and Google Play’s **Data Safety** truthfully (SDKs, data types, purposes, sharing).
- [ ] **App Store Review Guidelines**: read end-to-end; focus on **1.2 (UGC)**, **5.1 (Privacy)**, **Sign in with Apple**, **account deletion** (initiate inside app).
- [ ] If you use ad tracking or certain SDKs, implement **App Tracking Transparency (ATT)** prompts on iOS.

> Permissions

- [ ] **Location** (foreground; **background only if truly necessary** for “nearby events” even when app is closed; otherwise avoid).
- [ ] **Notifications** (Android 13+ needs runtime permission; iOS requires user consent).
- [ ] **Photos/Media**, **Camera**, **Contacts** only if you actually use them—explain the purpose in-app.

> Build targets

- [ ] **Android**: meet Play’s **target API** deadline. New apps/updates must target **Android 15 (API 35) from Aug 31, 2025**.
- [ ] **iOS**: support current iOS; include **Sign in with Apple** if you offer third-party logins (policy keeps shifting, but adding it avoids friction)

> Store Assets

- [ ] **Play**: app icon **512×512 PNG**, feature graphic **1024×500**, compliant screenshots.
- [ ] **App Store**: required iPhone (6.7″ or 6.5″) + iPad screenshots (check current spec table).

> Observability and Reliability

- [ ] Crash reports (sentry/firebase crashlytics)
- [ ] Logging Metrics and Google Analytics.

## Fix Cost

| Item                              | Cost (approx)                                 | Notes                                                                                                                  |
| --------------------------------- | --------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **Google Play Developer Account** | **$25 one-time**                              | One-off; tied to your org’s Gmail.                                                                                     |
| **Apple Developer Program**       | **$99/year**                                  | Mandatory for App Store publishing.                                                                                    |
| **Domain & Hosting for Policies** | **$10–20/year** (domain) + hosting ($5–10/mo) | Privacy policy, terms, refund policy must be online. You already have `thescenezone.com`, so just hosting/maintenance. |
| **Backend Hosting (MERN)**        | **$20–50/month** to start                     | e.g. Render, Railway, Heroku, DigitalOcean, AWS Lightsail. Scales with traffic.                                        |
| **MongoDB Atlas (DB hosting)**    | Free tier → $9–25/month for production        | Free tier not ideal for prod; budget for a shared cluster.                                                             |
| **CDN / SSL**                     | Often free (Cloudflare, Let’s Encrypt)        | Stores require secure HTTPS API endpoints.                                                                             |

