# GI Joe & Jane's Availability Calendar

A live, shared availability calendar for our group to find open weekends and plan trips. Built with vanilla HTML/CSS/JS and Firebase Firestore for real-time sync.

🔗 **Live site:** https://yourusername.github.io/squad-availability/

---

## What it does

- **Everyone adds their own dates** — select your name, dates, and a reason (wedding, travel, etc.)
- **Live sync via Firebase** — entries save instantly and show up for everyone the moment they're added
- **Auto-ranks the best trip windows** — the site finds open 6–7 day slots and surfaces the top 5, prioritizing windows that cover full weekends and federal holidays
- **Scrollable across years** — plan ahead through 2032
- **Federal holidays auto-calculated** for every year (Memorial Day, Labor Day, Thanksgiving, etc.)

---

## How to use it

### Adding your dates
1. Open the site on any device
2. Tap **✦ Add Your Dates**
3. Select your name, pick a start/end date, add a reason
4. Hit **Add to Calendar** — done. Everyone else sees it immediately.

### Reading the calendar
- 🟢 **Green days** = open weekends (nobody busy)
- 🟡 **Yellow days** = some conflicts
- 🔴 **Red days** = heavy conflicts (3+ people busy)
- 🔵 **Blue dashed outline** = US federal holiday
- Hover/tap any day to see who's busy and why

### Removing an entry
Scroll to "Submitted entries" in the add panel and tap **remove** next to any entry.

---

## Pre-loaded group events

These apply to everyone and are baked into the site:
- **May 6–10, 2026** — Dev Modi's Wedding
- **June 19–20, 2026** — Pratik and Nidhi's Engagement
- **July 11–12, 2026** — Vishesh and Neha's Engagement

---

## Setup (for the repo owner)

### 1. Deploy to GitHub Pages
1. Fork or clone this repo
2. Make sure the file is named `index.html`
3. Go to **Settings → Pages**
4. Under "Source," choose **Deploy from a branch**, pick `main` → `/root` → Save
5. Your site will be live at `https://yourusername.github.io/repo-name/` within a minute

### 2. Firebase config
The Firebase config is embedded in `index.html`. If you want to use your own Firestore project:

1. Create a project at [firebase.google.com](https://firebase.google.com)
2. Enable **Firestore Database** (start in test mode)
3. Under **Project settings → Your apps**, register a web app and copy the config
4. Replace the `firebaseConfig` block in `index.html` with yours
5. Under **Firestore → Rules**, set:

   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /{document=**} {
         allow read, write: if true;
       }
     }
   }
   ```

   ⚠ **Important:** Firebase's default "test mode" rules expire after 30 days. Set the rules above before that happens or the site will stop saving entries.

### 3. (Optional) Add your domain to Firebase
If you add Firebase Authentication later, go to **Build → Authentication → Settings → Authorized domains** and add `yourusername.github.io`.

---

## Tech stack

- **Frontend:** Vanilla HTML, CSS, and JavaScript — no build step, no framework
- **Fonts:** DM Serif Display (display) + DM Mono (body) via Google Fonts
- **Database:** Firebase Firestore (free tier is more than enough for a small group)
- **Hosting:** GitHub Pages

---

## Privacy note

The Firestore database is currently open to anyone who has the link — there's no authentication. This is fine for a private, unpublished group link, but don't post the URL publicly or bots will find it. If you ever want to lock it down, add Firebase Anonymous Auth and update the rules to `allow read, write: if request.auth != null`.

---

## License

Private — built for the squad.
