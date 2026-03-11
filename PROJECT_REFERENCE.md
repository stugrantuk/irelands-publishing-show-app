# Ireland's Publishing Show App — Project Reference

**Last updated:** March 2026  
**Purpose:** This document explains exactly how the app works so that any future AI session can make changes quickly and correctly.

---

## How the App Works (Critical — Read This First)

The app is a **static HTML web app** hosted on **GitHub Pages**. It is wrapped into native iOS and Android apps using **AppMySite**.

**The flow is:**

```
You edit files → Push to GitHub → GitHub Pages auto-deploys → AppMySite loads the updated web app → Users see changes instantly
```

There is **no build step, no recompiling, no App Store resubmission needed** for content changes. Changes go live within 1–2 minutes of pushing to GitHub.

---

## The Correct Repository

**IMPORTANT:** There are TWO repositories. Only one controls the live app.

| Repo | Purpose | Edit this? |
|------|---------|-----------|
| `stugrantuk/irelands-publishing-show-app` | **THE LIVE APP** — this is what AppMySite serves | ✅ YES |
| `stugrantuk/irelands-publishing-show` | Manus internal project (React Native / Expo) — NOT used by the live app | ❌ NO |

**Live app URL:** https://stugrantuk.github.io/irelands-publishing-show-app/

---

## Repository Structure

```
irelands-publishing-show-app/
├── index.html          ← Home screen
├── schedule.html       ← Schedule (all 3 days) — most commonly edited
├── speakers.html       ← Speakers list
├── vendors.html        ← Sponsors & vendors
├── info.html           ← General info / venue
├── styles.css          ← All styling
├── ips-logo.png        ← App logo
└── PROJECT_REFERENCE.md ← This file
```

---

## How to Clone and Edit

### Step 1 — Clone the correct repo

```bash
git clone https://github.com/stugrantuk/irelands-publishing-show-app.git
cd irelands-publishing-show-app
```

### Step 2 — Make your edits

Edit the relevant HTML file directly. The files are plain HTML — no framework, no build tools.

### Step 3 — Push to GitHub

You will need a GitHub Personal Access Token (PAT) to push. The owner is **stugrantuk**.

```bash
git add .
git commit -m "Description of your change"
git push https://YOUR_GITHUB_TOKEN@github.com/stugrantuk/irelands-publishing-show-app.git main
```

To get a token: GitHub → Settings → Developer Settings → Personal Access Tokens → Generate new token → tick **repo** scope.

---

## How to Get a GitHub Token (if needed)

1. Go to https://github.com/settings/tokens/new
2. Note: type any name (e.g. `manus-push`)
3. Tick the **repo** checkbox
4. Click **Generate token**
5. Copy the token (starts with `ghp_`) — use it in the push command above

GitHub will ask for identity verification via email OTP before generating the token.

---

## Schedule Structure (schedule.html)

The schedule is divided into 3 day sections using `<div class="card">` blocks:

- **Tuesday 17th March** — Evening only (check-in, drinks, party)
- **Wednesday 18th March — Day 1** — Full day with Main Room + Room Two
- **Thursday 19th March — Day 2** — Full day with Main Room + Room Two

### Session HTML Pattern

```html
<div class="session-item" data-session="UNIQUE-ID">
  <span class="heart-icon inactive" onclick="toggleSession('UNIQUE-ID')">♡</span>
  <span class="session-time">HH:MM</span>
  <h3>Session Title</h3>
  <p><strong>Speaker:</strong> Speaker Name</p>
  <p class="session-room">📍 Room Name</p>
</div>
```

- `data-session` must be **unique** across the entire file (used for favouriting)
- Break/meal rows use class `break-item` (dark green background, no heart)
- Room Two sessions also have `<span class="room-badge">Room Two</span>`

### Break/Meal Pattern

```html
<div class="session-item break-item" data-session="UNIQUE-ID">
  <span class="session-time">HH:MM</span>
  <h3>☕ Morning Break</h3>
</div>
```

---

## The Event

**Ireland's Publishing Show 2026**  
**Dates:** Tuesday 17 – Thursday 19 March 2026  
**Organiser:** Go Do World Ltd / Indie Network Events  
**Contact:** irelandspublishingshow@gmail.com  
**Main sponsor:** Digital Authors Toolkit (created the app)

### App Store Links

| Platform | Link |
|----------|------|
| iOS (Apple) | https://apps.apple.com/app/id6759912914 |
| Android (Google Play) | https://play.google.com/store/apps/details?id=app.irelandspublishingshow.android |

---

## AppMySite

The native app wrappers (iOS + Android) were created using **AppMySite** (https://www.appmysite.com). AppMySite points to the GitHub Pages URL and wraps it as a native app. No changes to AppMySite are needed for content updates — only for structural/design changes to the app shell itself.

---

## Apple App Store — EU Availability Fix (March 2026)

The app was initially unavailable in Ireland and EU countries due to missing **Digital Services Act (DSA)** compliance. This was fixed by:

1. Going to App Store Connect → Business → Agreements
2. Selecting **"I'm a trader under the DSA"**
3. Entering Go Do World Ltd contact details

This is now active and the app is available in all 175 countries.

---

## Common Tasks

### Update the schedule
Edit `schedule.html` — find the relevant day/session and update the title, speaker, or time. Push to GitHub.

### Add a new session
Copy an existing `session-item` div, give it a new unique `data-session` ID, update the content. Push to GitHub.

### Update a speaker name
Find the speaker name in `schedule.html` and/or `speakers.html` and update. Push to GitHub.

### Add a new speaker
Add a new entry to `speakers.html` following the existing pattern. Push to GitHub.

### Update sponsors/vendors
Edit `vendors.html`. Push to GitHub.

---

## Notes

- Changes are live within **1–2 minutes** of pushing to GitHub (GitHub Pages deployment time)
- Users need to **force-close and reopen** the app to see updates (or wait for the app to refresh)
- The favouriting/agenda feature uses **localStorage** in the browser — it persists per device
- Do NOT edit the `stugrantuk/irelands-publishing-show` Manus repo for live app changes — it has no effect on the live app
