# 1. ThemeGPT Premium 1.0 – Product Spec

### 1.1 Objectives

* Keep the **free extension** simple: just theme switching (as in v1.0.1).
* Offer **premium themes** that can be purchased individually or via subscription.
* Maintain a **zero-tracking, minimal data** stance:

  * The extension does not collect or send usage data.
  * Website only collects what’s required for payments (Stripe) and does not profile or resell user data.
* Provide **one-click theme delivery** from website to extension:

  * No manual file downloads or uploads.
  * Purchased themes just appear under a clearly labeled “Premium” or “Purchased” section in the popup.

---

### 1.2 Premium Features (Extension Side)

For Premium users, the extension gains:

* A new section in the popup:

  * `Free Themes` (current presets)
  * `Premium Themes` (purchased or subscription-access themes)

* A “Connect to ThemeGPT” onboarding step:

  * The extension can be “linked” to the website via a **secure anonymous token**, not a user account.
  * Once linked, the extension can fetch a list of purchased themes from the ThemeGPT API.

* 1-click apply for premium themes (same UX as free ones).

No advanced editor, marketplace, or creator upload is required in Premium v1—just **delivery of curated premium themes**.

---

### 1.3 Premium Features (Website Side)

Use theme-gpt.ai to provide:

* A public **themes catalog** (free + paid).
* A simple **checkout**:

  * Option A: one-off purchase `$0.99 / theme`
  * Option B: subscription `$1.99 / month` for 3 theme credits
* A **“Send to my extension”** button after purchase, which:

  * Detects if the extension is installed
  * Sends the purchased theme info to the extension via a content script / postMessage bridge
* A minimal **“Manage themes”** page:

  * Lists themes associated with that token (or account, if you later decide to add login)

---

### 1.4 Identity & Privacy Model

You explicitly want:

* No tracking, no data harvesting.
* As seamless as possible, but not at the cost of privacy.

A pragmatic compromise:

* The **extension remains anonymous**:

  * It generates a random `client_token` (UUID) on first run and stores it in `chrome.storage.sync`.
  * This token never encodes email; it’s just a random ID.

* The **website sees two identifiers**:

  * A Stripe customer ID (stored privately in your backend).
  * The `client_token` during the “Send to extension” flow, used only to associate purchases with that browser.

* You do not:

  * Track browsing.
  * Log ChatGPT content or user prompts.
  * Share data with third parties beyond payment processing.

This lets you reliably send themes to **that** browser’s extension without tying it to a full-blown user account if you don’t want to.

If in the future you want cross-device sync, that’s when you can introduce an optional **login** or “connect email” step—but it’s not required in v1.

---

## 2. Architecture Overview (Premium v1)

### 2.1 Components

* **Chrome Extension (ThemeGPT v2.x)**

  * Adds premium theme list + “Connect” mechanism.
  * Makes HTTPS calls to `https://api.theme-gpt.ai/...` for theme metadata.

* **Website (theme-gpt.ai, on WordPress)**

  * Front-of-house UI: catalog, pricing, pages.
  * Integrates Stripe Checkout (via plugin or a custom integration).
  * API plugin or a small companion service to expose purchase → theme mapping.

* **Backend API (could be WP plugin or small Node/Strapi service)**

  * Endpoints:

    * `POST /connect` — link extension `client_token` with Stripe customer or anonymous purchase session.
    * `GET /themes?client_token=...` — return list of theme IDs and metadata the extension can display.
    * `GET /theme/:id/json?client_token=...` — return theme JSON variables for that client if they own it.

* **Stripe**

  * One-off checkouts for single themes.
  * Subscriptions for monthly credit plans.

---

### 2.2 Critical UX Flow: One-Click Theme Delivery

Goal: user clicks “Buy” on the site → theme appears inside extension in seconds.

Proposed flow:

1. User installs extension (free).
2. In the extension popup, user clicks: **“Connect to ThemeGPT.ai”**.

   * Extension generates/stores `client_token`.
   * Extension opens `https://theme-gpt.ai/connect?token=<client_token>` in a new tab.
3. Website `connect` page:

   * Reads `token` from query params.
   * Stores it server-side in a table `clients(client_token, created_at, last_seen_at)`.
4. User browses themes, clicks “Buy”:

   * Stripe checkout completes, returns to `https://theme-gpt.ai/thanks?token=<client_token>`.
   * Backend:

     * Logs in DB: `purchases(client_token, theme_id, price_cents, stripe_event_id, created_at)`
5. Website shows a “Send to extension” state:

   * Page JS runs `window.postMessage({ type: 'THEMEGPT_PURCHASED', themes: [...] }, '*')`.
6. Extension content script (matching `https://theme-gpt.ai/*`):

   * Listens for the postMessage.
   * On receipt, calls `chrome.runtime.sendMessage` to the background/popup.
   * Extension updates `chrome.storage.sync` with the new theme IDs and immediately fetches their JSON from `https://api.theme-gpt.ai/themes?client_token=...`.
7. In the popup UI:

   * Premium themes appear under “Purchased Themes”.
   * User clicks → theme applies.

This satisfies your constraint: **no local file download/upload** and a “just appears” feeling.

---

### 2.3 Theming Data Format

Keep premium themes as data, not code:

* Each theme = JSON like:

  ```json
  {
    "id": "christmas-cozy-01",
    "name": "Cozy Christmas",
    "category": "seasonal",
    "colors": {
      "--cgpt-bg": "#0b1a12",
      "--cgpt-surface": "#112016",
      "--cgpt-text": "#f6f3ee",
      "--cgpt-accent": "#e63946",
      "--cgpt-accent-contrast": "#07130d"
    }
  }
  ```

* Extension maps this JSON into CSS variable overrides.

* No remote JS, only CSS variables from the JSON; this keeps you in a safe place with Chrome policies.

---

## 3. Website Plan (WordPress + Existing Landing Concept)

You already have a strong landing-page concept with hero, features, pricing, and theme previews.

You can repurpose that into a WordPress theme:

### 3.1 Key Pages

1. **Home / Landing (theme-gpt.ai)**

   * Hero: “Transform Your ChatGPT Experience”
   * CTA buttons:

     * “Install Free Extension” (Chrome Web Store link)
     * “Browse Premium Themes” (catalog)

2. **Themes Catalog**

   * Grid of themes (with filters: Free, Christmas, Seasonal, Dark, Minimal).
   * Each card:

     * Name, preview, price (Free / $0.99).
     * “Preview” and “Buy / Add” buttons.

3. **Pricing / Membership**

   * Explains:

     * Free plan (current extension)
     * Subscription: `$1.99 / month` → can download 3 themes per month
     * One-off purchases: `$0.99` per theme.

4. **Connect Page**

   * Used in the flow when extension opens `/connect?token=...`.
   * Text like: “Your ThemeGPT extension is now connected. Browse themes below and they’ll appear in your extension as you purchase.”

5. **Support / FAQ**

   * Privacy: “No tracking, no personal data in the extension.”
   * Explains how purchases work, refunds, etc.

---

## 4. Aligning with Your Action Items

From your notes:

* Create specification documents for premium version upgrade
* Research and determine website design and style
* Build the theme-gpt.ai website
* Develop at least six Christmas themes
* Create seasonal themes for January through April

Here’s how I’d order it:

### Phase 1 – Specs and Architecture (what we just did)

* Lock **Premium v1 spec** (this doc).
* Finalize flows:

  * Free vs Premium behavior in extension.
  * `client_token` and API endpoints.
  * Checkout and Stripe integration.

Outcome: “ThemeGPT Premium 1.0 – Spec” doc ready.

### Phase 2 – Website Design & Build

* Adapt your existing HTML concept into a WordPress theme or child theme.
* Implement:

  * Hero, features, pricing, and simple catalog page.
  * A very basic custom plugin for:

    * Theme post type
    * Client token registration
    * Purchase → theme association APIs.

### Phase 3 – Extension Premium Integration

* Add:

  * Connect button and client_token generation.
  * “Premium / Purchased Themes” section in popup.
  * Content script for `theme-gpt.ai` to receive postMessages.
  * API calls to fetch purchased themes.

Release as ThemeGPT v2.0.0 (still free in the Store; premium is unlocked via website).

### Phase 4 – Themes Production

* Build at least six **Christmas** themes:

  * Red/green variants, some cozy, some bold.
* Build **January–April** seasonal themes:

  * January: cool winter blues / snow.
  * February: soft pinks / Valentine palette.
  * March: greens / clover, early spring.
  * April: pastel spring/Easter.

Each theme is just a JSON record + CSS variable mapping.

---

## 5. What You Might Want From Me Next

If you’d like, I can:

* Turn this into a more formal **Premium v1 PRD** with headings and numbered requirements.
* Draft the **API contract** (`/connect`, `/themes`, `/theme/:id`) you can hand directly to a backend implementation (even if it’s a WP plugin).
* Or sketch the **extension UI changes** (popup layout wireframe) to show exactly where “Purchased Themes” will live.

Tell me which of those you want first, and I’ll draft it in a ready-to-use format.
