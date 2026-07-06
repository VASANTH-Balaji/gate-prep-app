# Building the Signed Debug APK

## What's already done for you
- `capacitor.config.json` — app ID `com.gateprep.app`, app name "GATE Prep", web dir `dist`
- `package.json` — `@capacitor/core`, `@capacitor/android`, `@capacitor/cli` added
- `android/` — full Capacitor Android project scaffold (Gradle files, manifest, `MainActivity.java`, launcher icons generated in your brand color `#2451C4`, adaptive icon XML, FileProvider config)
- `android/app/debug.keystore` — a **real, already-generated** debug signing keystore (alias `androiddebugkey`, password `android` — the Android default). `android/app/build.gradle` is wired to sign `debug` builds with it automatically.
  - SHA1: `A9:E4:55:F4:41:55:94:A1:F7:EF:33:53:55:AD:7A:AC:BC:4D:7C:7E`
  - SHA256: `6F:A4:CC:00:B8:50:92:46:BA:39:30:D6:01:F1:DE:22:0B:30:AF:70:DF:AC:80:40:66:D9:1B:D7:82:B6:53:C8`

## What you need to run locally (2 commands)
I built this in a sandbox with no network access and no Android SDK, so I could hand-author every config/source file but couldn't fetch npm packages, download the Gradle distribution, or invoke the Android build toolchain myself. Two things need your machine:

```bash
npm install                     # pulls in @capacitor/core, @capacitor/android, @capacitor/cli
npm run build                   # vite build -> dist/
npx cap sync android            # copies dist/ into android/app/src/main/assets/public
                                 # and generates capacitor.settings.gradle / capacitor.build.gradle
```

Then build the APK:

```bash
cd android
./gradlew assembleDebug
```

The signed APK will be at:
```
android/app/build/outputs/apk/debug/app-debug.apk
```

## One gotcha: the Gradle wrapper jar
`android/gradle/wrapper/gradle-wrapper.jar` is a compiled binary that ships with Gradle itself — I can't generate it from a sandbox with no network or Gradle install. Two easy fixes, pick either:

1. **Open the project in Android Studio** — it detects the missing wrapper jar and regenerates it automatically on project sync.
2. **If you have Gradle installed locally**, run once from the `android/` folder:
   ```bash
   gradle wrapper --gradle-version 8.7
   ```

After that, `./gradlew assembleDebug` will work standalone.

## Verifying the signature (optional)
```bash
keytool -list -v -keystore android/app/debug.keystore -storepass android
```
should print the fingerprints above.
