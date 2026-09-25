# Guessle download page

A static single-page site that serves `guessle.apk`. There's no build step.

## Deploy to Vercel

**CLI**, from this folder:

```powershell
npm i -g vercel
vercel          # first time: log in, accept defaults
vercel --prod
```

**Dashboard:** push the repo to GitHub, import it in Vercel, and set **Root Directory** to
`download_web`. Set Framework Preset to **Other** and leave the build command empty.

## Releasing a new version

From the project root:

```powershell
# 64-bit phones only: keeps the APK under GitHub's 25 MB web-upload limit
flutter build apk --release --target-platform android-arm64
Copy-Item build\app\outputs\flutter-apk\app-release.apk download_web\guessle.apk -Force
```

Then bump the version text in `index.html` (search for `Version 1.0.0`) and redeploy.
The page reads the file size from the APK automatically.

## Files

- `index.html`: the page. Android visitors see the download button. Desktop visitors also
  see a QR code to open the page on their phone.
- `guessle.apk`: the app.
- `vercel.json`: serves the APK with the Android package content type and forces a download.
