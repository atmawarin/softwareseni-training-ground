# Vision & Primary KPI

File: `/business-context/01-vision-and-kpi.md` • Version: 1.3 • Last Updated: 2025-08-19

This document combines the **Vision & Business Context** and the **Primary KPIs** for the Women Empowerment social platform. It aligns with the Blueprint vision and the signed SoW scope for a **working MVP web prototype**.

---

## 1\) Vision & Business Context

### 1.1 Problem & Opportunity

- **User pains.** Women lack a safe, supportive space to share personal stories without “mom-shaming,” struggle to find meaningful interactions, and need private, empathetic guidance.  
- **Admin pains.** The platform must be trusted and scalable with effective moderation and responsible data handling.  
- **Opportunity.** Deliver a mobile-first, supportive community where women can share (anonymous or public), join communities, and receive empathetic support—establishing the foundation for future growth.

### 1.2 Mission Statement

Deliver a **working MVP web prototype** of **Sista**—a safe, inclusive, AI-aware community for women—so stakeholders can validate core user interactions and decide on a full MVP build. This phase emphasizes rapid value while maintaining essential quality and basic data safety.

### 1.3 Target Audience & Roles (summary)

- **End Users (women 18–45).** Create accounts, manage profile/alias, post anonymously or publicly, join communities, interact (comment, Hug), send DM, manage privacy and account deletion.  
- **Administrators (future CMS).** Moderate content, manage communities, and oversee user/content operations (note: CMS is *not* in scope this phase; listed for future alignment).

### 1.4 Value Proposition & Differentiators

- **Anonymous posting** with supportive reactions (e.g., “Hug/aku pernah”), comments, and reporting tools.  
- **Curated communities** with discovery, highlights, and healthy public interactions.  
- **Mobile-first UX** with clear navigation and timely notifications.  
- **Safety & privacy first** within prototype constraints (sensible auth, rate limiting, basic safeguards).

### 1.5 Scope — This Phase (Aligned to SoW)

**Included (working MVP web prototype):**

- **Authentication** (register, login, forgot/change password, email verification).  
- **Profile & Settings** (alias, basic privacy, delete account).  
- **Anonymous**: post, comment, reactions (“Hug/aku pernah”), DM, block, report.  
- **Communities**: community feed/highlight, public interactions, discovery/search.  
- **Moderation (basic)**: owner & admin can report/flag/block/delete posts.  
- **Notifications**: real-time alerts, read/unread, notification history.  
- **Design/UI**: mobile-first, bottom navigation, component styling.  
- **QA & Deployment**: SIT, final QA, deploy to a stable test environment.

**Explicitly out of scope (this phase):**

- Admin/CMS backend and internal moderation tools.  
- Payments, email marketing, or other 3rd-party integrations not listed above.  
- Advanced features: daily tips, video/voice, mentorship, **Ask Sista AI chat**, gamification/badges.  
- Native mobile apps, production-grade DevOps/security audits, and large-scale performance work.

### 1.6 Delivery Principles

- **Safety-first & privacy-by-design** for the prototype’s scope.  
- Up to **3× minor review sessions** (text/visual tweaks, simple flow polish, and light bug fixes). Any major change is handled via **change request** with separate estimate.

### 1.7 Core Journeys to Validate (Prototype)

1) **Auth** → onboarding/profile/alias → verified access.  
2) **Anonymous posting** → comments & reactions → reporting/blocking when needed.  
3) **Communities** → discover → join → interact.  
4) **Notifications** → real-time updates → inbox/history.

### 1.8 Success Criteria (End of Phase Deliverables)

- Accessible **working MVP web** in a stable test environment (URL shared).  
- **Feature list** above working end-to-end with basic safeguards.  
- **Short usage notes** (how to navigate & test flows).  
- **Final technical notes** (what’s built, known limitations).

### 1.9 Assumptions & Risks

**Assumptions.**

- Brand assets and copy are provided.  
- No external integrations beyond the listed scope.  
- Prototype is web-based (mobile-first layout), not native mobile.

**Risks.**

- Scope creep beyond minor reviews (addressed via change requests).  
- Sensitivity of mental-health topics requires careful tone & moderation guidance.  
- Without a CMS in this phase, moderation relies on basic in-app controls by post owners and limited admin actions.

---

## 2\) Primary KPI

The KPIs below validate the working MVP prototype (not production scale).

### 2.0 Target Assumptions

- **Pilot cohort:** \~**150–300** invited accounts in the first 2–3 weeks.  
- **Evaluation window:** weekly rollups; first read after **Week 2**.  
- **Support hours:** moderation SLA measured during **09:00–18:00 WIB (business days)**.  
- **Small team:** operational processes are lightweight; targets are intentionally conservative for MVP.

### 2.1 KPI Summary (with Targets)

| Category | KPI | Definition | Formula | Instrumentation (event / properties) | Owner | Target | Notes |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| Acquisition | Registrations | \# users who complete sign-up | `count(auth_register_success)` | `auth_register_success` | PM/Analytics | **≥150** (by end of Week 2\) | Unique by email |
| Acquisition | Email Verification Rate | Share of sign-ups that verify email | `email_verify_success ÷ auth_register_success` | `email_verify_success` | PM/Analytics | **≥75%** | 24h window |
| Activation | Onboarding Completion | % users completing alias/profile | `onboarding_complete ÷ auth_register_success` | `onboarding_complete` | PM/Analytics | **≥70%** | First session |
| Activation | First Anonymous Post | % active users posting ≥1 anonymous post (wk) | `distinct_users(post_create_success{anon:true}) ÷ WAU` | `post_create_success { anon: true }` | Product | **≥25%** | Weekly window |
| Activation | First Community Join | % active users joining any community (wk) | `distinct_users(community_join) ÷ WAU` | `community_join` | Product | **≥40%** | — |
| Engagement | Comments per Post | Avg comments per anonymous post | `comment_create_success ÷ post_create_success{anon:true}` | `comment_create_success` | Product | **≥1.0** | Weekly |
| Engagement | “Hug” Reaction Rate | Avg hugs per post | `reaction_hug ÷ post_create_success` | `reaction_hug` | Product | **≥1.5** | — |
| Safety & Trust | Report Rate | Reports per 1,000 posts | `(content_report ÷ post_create_success) × 1000` | `content_report { reason:string }` | Safety/PM | **≤20 / 1,000** | Track by type |
| Safety & Trust | Report→Action SLA | Median minutes from report to action | `median(t_action − t_report)` | `moderation_action`, `content_report` | Safety | **≤120 min** (biz hrs) | Prototype SLA |
| Reliability | Crash-free Sessions | % sessions without a crash | `1 − (crash_sessions ÷ total_sessions)` | Client crash logs | QA | **≥99.0%** | Weekly |
| Notifications | Delivery Success | % notifications delivered | `notification_delivered ÷ notification_sent` | `notification_sent`, `notification_delivered` | Engineering | **≥95%** | By channel |

### 2.2 KPI Details

**Registrations**

- Category: Acquisition • Definition: successful sign-ups.  
- Formula: `count(auth_register_success)` • Events: `auth_register_success`  
- Owner: PM/Analytics • Reporting: daily & weekly • **Target: ≥150 by end of Week 2** • Notes: unique by email; exclude bot traffic if detected.

**Email Verification Rate**

- Category: Acquisition • Definition: % of sign-ups verifying email within 24h.  
- Formula: `email_verify_success ÷ auth_register_success` • Events: `email_verify_success`  
- Owner: PM/Analytics • Reporting: daily & weekly • **Target: ≥75%**

**Onboarding Completion**

- Category: Activation • Definition: % of new users completing alias/profile in 1st session.  
- Formula: `onboarding_complete ÷ auth_register_success` • Events: `onboarding_complete`  
- Owner: PM/Analytics • Reporting: weekly • **Target: ≥70%**

**First Anonymous Post**

- Category: Activation • Definition: % of WAU creating ≥1 anonymous post.  
- Formula: `distinct_users(post_create_success{anon:true}) ÷ WAU` • Events: `post_create_success { anon:boolean }`  
- Owner: Product • Reporting: weekly • **Target: ≥25%**

**First Community Join**

- Category: Activation • Definition: % of WAU joining any community.  
- Formula: `distinct_users(community_join) ÷ WAU` • Events: `community_join`  
- Owner: Product • Reporting: weekly • **Target: ≥40%**

**Comments per Post**

- Category: Engagement • Definition: avg comments per anonymous post.  
- Formula: `comment_create_success ÷ post_create_success{anon:true}` • Events: `comment_create_success`  
- Owner: Product • Reporting: weekly • **Target: ≥1.0**

**“Hug” Reaction Rate**

- Category: Engagement • Definition: avg “Hug” reactions per post.  
- Formula: `reaction_hug ÷ post_create_success` • Events: `reaction_hug`  
- Owner: Product • Reporting: weekly • **Target: ≥1.5**

**Report Rate**

- Category: Safety & Trust • Definition: reports per 1,000 posts.  
- Formula: `(content_report ÷ post_create_success) × 1000` • Events: `content_report { reason:string }`  
- Owner: Safety/PM • Reporting: weekly • **Target: ≤20 / 1,000 posts**

**Report→Action SLA**

- Category: Safety & Trust • Definition: median minutes from report to action.  
- Formula: `median(moderation_action.timestamp − content_report.timestamp)` • Events: `moderation_action { action:string }`, `content_report`  
- Owner: Safety • Reporting: weekly • **Target: ≤120 minutes (business hours)**

**Crash-free Sessions**

- Category: Reliability • Definition: % sessions without crash.  
- Formula: `1 − (crash_sessions ÷ total_sessions)` • Events: client crash logs  
- Owner: QA • Reporting: weekly • **Target: ≥99.0%**

**Notification Delivery Success**

- Category: Notifications • Definition: % notifications delivered (by channel).  
- Formula: `notification_delivered ÷ notification_sent` • Events: `notification_sent { channel:string }`, `notification_delivered { channel:string }`  
- Owner: Engineering • Reporting: weekly • **Target: ≥95%**

### 2.3 Event Dictionary (Starter)

auth\_register\_success

email\_verify\_success

onboarding\_complete

post\_create\_success { anon:boolean }

comment\_create\_success

reaction\_hug

community\_join

content\_report { reason:string }

moderation\_action { action:string }

notification\_sent { channel:string }

notification\_delivered { channel:string }

### 2.4 Reporting & Governance

- **Cadence:** daily pulse (automated), weekly review in sprint ritual.  
- **Dashboards:** Acquisition/Activation, Engagement, Safety, Reliability, Notifications.  
- **Data Quality:** event names in lower\_snake\_case; required properties enforced; UTC timestamps; dedupe by user\_id \+ session\_id.

### 2.5 Notes & Exclusions

- KPIs reflect **current MVP prototype scope** per SoW.  
- Out-of-scope items (CMS/admin, payments, badges, voice/video, advanced AI chat) are **not** included in the primary KPI set.

## Update

* **Vision**: Deliver Sista MVP — a safe, inclusive, mobile-first community for women to share anonymously or publicly, join curated communities, and receive empathetic support.    
* **Problem**: Women lack stigma-free spaces to share stories; current platforms fail on safety and meaningful interaction.    
* **Opportunity**: Build trust-first platform for supportive expression \+ curated communities → foundation for future growth.    
* **Target Audience**: Women 18–45, especially students, early career professionals, and young mothers.    
* **Value Proposition**: Anonymous supportive posting, curated communities, safe interactions, and mobile-first design.    
* **Phase Scope (Prototype):**   
  * Auth  
  * Profile/alias  
  * Anonymous posts/reactions  
  * DMs  
  * Communities  
  * Basic moderation  
  * Notifications.    
* **Primary KPIs:**    
  * Registrations ≥150 by Week 2    
  * Email Verification ≥75%    
  * Onboarding Completion ≥70%    
  * First Anonymous Post ≥25% WAU    
  * First Community Join ≥40% WAU    
  * Avg Comments/Post ≥1.0    
  * Hug Reactions/Post ≥1.5    
  * Report Rate ≤20 / 1,000 posts    
  * Report→Action SLA ≤120 min    
  * Crash-free Sessions ≥99%    
  * Notification Delivery ≥95%

