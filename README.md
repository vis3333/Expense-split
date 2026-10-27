# SplitAI

A Splitwise / Tricount-style expense splitter with a modern glass UI and AI built in.

**Features**
- Groups, friends, equal / exact / percent splits, per-group balances
- Simplified settle-up (fewest payments) with "Mark paid"
- ✨ Plain-English entry: "Dinner 1200 paid by Raj with Anu" (offline parser, or Claude if a key is set)
- 📷 Receipt scan: photo of a bill becomes line items; tap who shared each item; tax and tip split proportionally
- 📊 Insights: category bars, top payer, averages, plus an AI money coach
- 💬 Assistant: ask "Who owes me?" or "What did we spend most on?"
- All data stays on the device (localStorage). Backup/restore from the More tab.

## Get the APK (easiest — no Android Studio)

1. Create a new GitHub repo and push this folder to it (`git init && git add . && git commit -m init && git push`).
2. Open the repo's **Actions** tab → **Build Android APK** → it runs automatically on push (or click *Run workflow*).
3. When it finishes (~5 min), open the run and download the **SplitAI-debug-apk** artifact. Unzip it and install `app-debug.apk` on your phone (allow "Install unknown apps").

## Build locally instead

Needs Node 20+, JDK 21 and Android Studio / the Android SDK.

```bash
npm install
npx cap add android
npx cap sync android
npx cap open android      # then Build → Build APK(s)
```
For the receipt camera, add `<uses-permission android:name="android.permission.CAMERA" />` to `android/app/src/main/AndroidManifest.xml`.

## Try it right now in a browser

```bash
npx serve www     # or: python3 -m http.server -d www
```
Open it on your phone's Chrome and use **Add to Home screen**.

## Turning on the AI features

Open **More → AI features** and paste a Claude API key (console.anthropic.com). It is stored only on your phone and calls go straight to Anthropic. Haiku 5.5 is fast and cheap; Sonnet 5.5 is smarter on messy receipts. Do not ship an APK with a key baked in — anyone could extract it. For a public release, put a small backend in front of the API.

## Release notes / next steps
- Debug APK is fine for personal use. For Play Store: create a keystore and run `./gradlew bundleRelease`.
- Sync across phones needs a backend (e.g. Supabase/Firebase) — not included.
- Replace `www/icon.svg` and generate launcher icons with `npx @capacitor/assets generate`.
