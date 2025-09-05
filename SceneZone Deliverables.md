# Deliverables & Milestones (functional)

## Phase I — Frontend stabilisation & Backend deployment (3 weeks)

**Dates:** **28 Aug 2025 → 18 Sep 2025** (21 calendar days)

**Functional deliverables**

1. **Frontend stability fixes**
    - Fix crashes so app runs for **≥ 30 minutes** under typical usage without crashing.
    - Stabilize **WebSocket** connections: auto-reconnect, exponential backoff, heartbeat/ping, and graceful handling of disconnects.
    - Fix navigation tree & backstack issues; enforce consistent navigation behavior across Android/iOS.
    - Fix keyboard overlay/margin issues so input fields are never hidden on portrait/landscape and across common devices.
    - Fix user flows flagged as broken (artist/host login flow) so login/signup/role-switching is consistent and reproducible.
    - Fix Razorpay integration errors in sandbox mode and implement clear client-side error handling and server-side webhook verification.
2. **Integration & testing**
    - End-to-end test flows for: sign-up/login (artist / host / fan), booking flow, ticket checkout (Razorpay in test mode), websocket-driven live updates, logout/cleanup.
    - Integrate crash reporting (Sentry / Firebase Crashlytics) and ensure crashes are reported with stack traces.
3. **Backend deployment & infra**
    - Dockerize backend services (if not already) and push images to **ECR**.
    - Deploy backend on **ECS** with autoscaling (CPU/Memory-based policies), Application Load Balancer with health checks.
    - Set up environment in **AWS**: IAM roles, Secrets Manager (or Parameter Store) for secrets, CloudWatch logs, CloudWatch alarms for error rates/ latency, automated snapshot/backups for DB (RDS or other).

**Acceptance criteria (Phase I)**

- App remains crash-free for simulated environment.
- WebSocket reconnects within 5 seconds after network blips and resumes updates.
- Razorpay flows succeed in sandbox environment and webhook reconciliation works in staging.
- Backend services pass health checks for 48 hours under light load; autoscaling triggers when load threshold is reached.
- CI pipeline builds + deploys to staging automatically on merge to `main` branch.

---

## Phase II — Data flow, permissions & policy readiness (1 week)

**Dates:** **19 Sep 2025 → 25 Sep 2025**

**Functional deliverables**

1. **Data flow diagram & permission matrix**
    
    - Complete data-flow diagrams for all user journeys (artist, host, fan, admin).
        
    - Permission/roles matrix clearly listing allowed API endpoints per role, data visibility rules, and escalation rules.
        
2. **Security & policy checklist**
    
    - Token/session management review (JWT expiry, refresh token flow, secure storage on mobile).
    - Privacy and data retention notes required for app store submissions (what personal data is collected, where it’s stored, how long retained).
        
3. **Compliance checklist for stores**
    
    - Google Play items: required privacy disclosures, payment disclosures, third-party SDK lists, tracking/transparency items.
        
    - List of required assets and metadata for store submissions (icons, screenshots, descriptions, privacy policy link).
        

**Acceptance criteria (Phase II)**

- Delivery of diagrams + permission matrix policies.
    
- Security checklist and remediation plan documented and prioritized (high/medium/low).
    

---

## Phase III — Play store preparation & submission (2 weeks)

**Dates:** **26 Sep 2025 → 9 Oct 2025**

> **Note:** This phase _starts only after_ DUNS + Google Play & Apple Developer accounts are available to the team. If accounts are delayed, dates will shift.

**Functional deliverables**

1. **Build & signing**
    
    - Create signed release APK / AAB. Provide keystore and instructions for key management (or sign with company key).
        
2. **Store-ready assets & metadata**
    
    - App icons, adaptive icons, screenshots for required device sizes, store descriptions, feature graphic, localized descriptions (if requested).
        
    - Privacy policy URL + in-app privacy disclosures filled.
        
3. **Submission & monitoring**
    
    - Submit to Google Play Console (internal test / closed track / production per request).
        
    - Submit to Apple App Store Connect (TestFlight then App Store).
        
    - Monitor review; address review issues / rejections and submit fix builds as required.
        

**Acceptance criteria (Phase III)**

- App accepted to Google Play internal/closed testing (or production if requested) and to TestFlight.
    
- Any store rejection issues logged and either resolved or have a mitigation/appeal plan.
    

---

## Phase IV — Post-deployment maintenance (2 weeks, non-functional)

**Dates:** **10 Oct 2025 → 23 Oct 2025**

**Functional deliverables**

1. **Bugfix SLA**
    
    - Fix critical/high priority bugs discovered after release (SLA: critical within 24 hours, high within 72 hours, medium/low in next sprint days).
        
2. **Monitoring & stabilisation**
    
    - Tune autoscaling and alarms based on real usage.
        
    - Minor UX/corner-case bug fixes (keyboard, tiny UX flows).
        

**Acceptance criteria (Phase IV)**

- Critical production incidents resolved per SLA.
    
- Crash rate reduced below agreed threshold (e.g., <0.5 crashes/user-hour or per acceptance test).

---
# Responsibilities & Who does what

- **Himanshu Aggarwal** — Lead dev for frontend + app builds, stabilization, E2E tests, CI/CD changes, and co-responsible for deployment tasks.
    
- **Rishav Kumar** — Co-developer, 50/50 split of development & support tasks (both sign-off responsibilities).
    
- **Scenezone** must provide: code repo access, staging servers/credentials, payment gateway sandbox keys, AWS account (or console access/role), test accounts, product owner for quick decisions, and legal/marketing for store materials.
    

---

# Access & assets required up front (before work starts)

- **Signed NDA + signed engagement contract** (as we drafted earlier).
    
- **Repository access:** read/write to the repo (GitHub/GitLab) and branch protection removal for initial deployment tasks, or an invitation to maintainers team.
    
- **CI/CD credentials** or ability to create GitHub Actions secrets.
    
- **AWS access:** either root-level billing admin for initial setup (NOT recommended) or an IAM user with required permissions (ECS, ECR, IAM, CloudWatch, RDS snapshots, Route53/ACM if needed).
    
- **Payment gateway test keys (Razorpay sandbox keys + webhook endpoint access)**.
    
- **App store account access** or admin to create required accounts (DUNS + Apple) — Phase III dependent.
    
- **Test accounts** for artist, host, and fan roles (staging/test users with sample data).
    
- **Domain & DNS access** if we need to point staging/prod endpoints or configure certificates.

---
# Risks & mitigations

1. **Account/credential delays (DUNS, Play Console, Apple Developer)**
    
    - _Mitigation:_ Start Phase II tasks that don’t require accounts; company to expedite DUNS and account creation. If delayed, Phase III dates will shift.
        
2. **Missing repo/tests or undocumented legacy code**
    
    - _Mitigation:_ Time-boxed reverse-engineer period (first 3 working days). If code is significantly broken/unmaintainable, scope & price will be revisited.
        
3. **Third-party (Razorpay / SDK) account issues or compliance**
    
    - _Mitigation:_ Work in sandbox; company must handle merchant onboarding and live keys.
        
4. **App store rejections for policy reasons**
    
    - _Mitigation:_ Use the compliance checklist in Phase II to reduce risk. Re-submission cycles may take unpredictable time.
        
