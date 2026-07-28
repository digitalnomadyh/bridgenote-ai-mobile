# BridgeNote AI -- Mobile Wrapper

A thin Capacitor Android shell around the deployed BridgeNote AI web app
(https://bridgenote-ai-pilot.streamlit.app/). It's just a WebView pointed at
that URL -- no UI rewrite -- so it always shows whatever is currently live on
Streamlit Cloud, and produces a real installable `.apk` you can share with
volunteers or pilot partners.

## Getting the APK (no local Android tooling required)

Every push to `main` triggers `.github/workflows/build-apk.yml`, which
compiles the app on GitHub's own runners (they already have Java + the
Android SDK installed) and uploads the result.

1. Push this repo to GitHub.
2. Go to the repo's **Actions** tab -> the latest "Build Android APK" run.
3. Download the `bridgenote-ai-debug-apk` artifact (a zip containing
   `app-debug.apk`).
4. Copy `app-debug.apk` to an Android phone/tablet and open it to install
   (the device will need "Install unknown apps" allowed for whichever app
   you used to transfer the file -- Files, Chrome, etc.).

This is a **debug build** (self-signed with Android's default debug key) --
perfect for sideloading testers during the pilot, but not accepted by the
Play Store. Submitting to the Play Store later would need a proper release
signing key and a $25 one-time Google Play developer account; ask if you
want that set up when you get there.

## Updating the target URL

Edit `server.url` in `capacitor.config.json`, then run:

```bash
npx cap sync android
```

and push -- the next Actions run will bake in the new URL.

## iOS

Not set up here -- building an `.ipa` requires a Mac with Xcode and an Apple
Developer account ($99/yr), which isn't available in this environment. The
same Capacitor project can add an iOS platform (`npx cap add ios`) later on
a Mac if that becomes a priority.
