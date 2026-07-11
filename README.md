# 🔥 My Routine

A morning/evening routine tracker built for one specific six-year-old, with real streaks, real money, and a live line straight to Dad. Single-file HTML, Firebase Realtime Database on the back end, deployed to GitHub Pages. No build step, no framework, no npm install, no recurring cost beyond a free-tier Firebase project.

## What it does

**For him:**
- Morning and evening checklists he taps through himself
- A streak flame that grows the more consecutive full days he completes
- Paid chores that unlock once the morning routine is done (not gated behind the whole day, because a tired kid at 8pm is not a productive kid)
- A confetti burst when he clears a routine
- Messages from Dad that show up right on his screen

**For me (dashboard, PIN-gated):**
- Live view of what's checked off today and over the last 7 days, no refreshing, no asking
- A running total of what I owe him, with a "Mark as Paid" button that resets it to $0 once I've actually paid
- Full control over both routine tasks and paid chores: add, edit, remove, set dollar values
- A message box that pushes straight to his screen

## The money logic

- Every 3-day streak pays $1 (day 3, 6, 9, 12...)
- Every 10-day streak adds a $5 bonus on top of that
- Money earned stays banked even if a streak breaks. Only future earning potential resets, not what he's already put in the bank
- Paid chores credit instantly when he taps them done, no approval queue slowing him down

## Tech stack

- Vanilla HTML/CSS/JS, one file, no build tooling
- Firebase Realtime Database for live sync between his tablet and my dashboard
- Firebase transactions (not simple reads/writes) on every balance update, so two taps at the same moment can't clobber each other
- Web-safe fonts via Google Fonts (Fredoka for headlines, Nunito for body text)

## Setup

1. Create a Firebase project and enable **Realtime Database**.
2. Register a Web App under Project Settings → General → "Your apps" and grab the config snippet.
3. Paste that config into the `firebaseConfig` object near the top of the `<script type="module">` block, replacing every `PASTE_YOUR_...` placeholder.
4. In the Realtime Database Rules tab, publish:
   ```json
   {
     "rules": {
       "routineTracker": {
         ".read": true,
         ".write": true
       }
     }
   }
   ```
5. Change `PARENT_PIN` in the script from the default `"1234"` to your own.
6. Push to GitHub Pages like the rest of the toolkit.
7. On the tablet: open the page in Safari, tap Share → Add to Home Screen.

## A note on privacy and security

This app runs with no authentication layer by design. It's meant for one family, on one Firebase project, with a URL only you and your kid know. The database rules above are scoped to a single path, not your whole database, but they're still open read/write to anyone who has the link. That's a fine trade-off for a home routine tracker. It is not a trade-off you should make for anything more sensitive, and this project should never be repointed at a Firebase database that holds anything else.

The PIN gate on the parent dashboard is a kid-deterrent, not real security. It lives in plain text in the page source. Perfectly fine for keeping a six-year-old out of the settings. Don't mistake it for anything stronger.

## Why this exists

Built during the same stretch of hyperfocus that produced many classroom tools, just pointed at a smaller and considerably more important student. If it gets him brushing his teeth without a fight and gives him a reason to feel proud of a streak, it's done its job.
