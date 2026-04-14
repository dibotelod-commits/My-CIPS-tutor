# CIPS 2026 Revision Hub: Final APK Build Commands

This document provides the definitive command sequence to build, sync, and generate a production-ready Android APK (API 27) for the CIPS 2026 Revision Hub.

---

## 1. Environment Preparation
Ensure you have Node.js, Android Studio (with SDK 27), and the Java Development Kit (JDK 11) installed.

```bash
# Verify versions
node -v
npm -v
java -version
```

## 2. Phase 1: Web Application Build
Transform your source code into production-ready web assets.

```bash
# 1. Install project dependencies
npm install

# 2. Compile web assets
# This creates the 'www' or 'dist' folder defined in capacitor.config.json
npm run build

# 3. (Optional) Manual copy if your build script doesn't target the 'www' folder
# mkdir -p www && cp -r dist/* www/
```

## 3. Phase 2: Capacitor Synchronization
Bridge the web assets with the native Android wrapper.

```bash
# 4. Sync web assets and plugins with the Android project
npx cap sync android

# 5. Update native dependencies
npx cap update android
```

## 4. Phase 3: APK Generation (CLI Method)
Generate the installer files directly from the terminal.

### Debug APK (For Testing)
```bash
# 6. Navigate to the android directory and build
cd android
./gradlew assembleDebug

# Output Path: 
# android/app/build/outputs/apk/debug/app-debug.apk
```

### Release APK (For Distribution)
*Note: This produces an unsigned APK. Follow the GitHub Copilot prompt provided earlier for automated signing via GitHub Actions.*

```bash
# 7. Generate the unsigned release bundle
./gradlew assembleRelease

# Output Path:
# android/app/build/outputs/apk/release/app-release-unsigned.apk
```

## 5. Phase 4: Manual Signing (If not using GitHub Actions)
If you need to sign the APK manually on your machine:

```bash
# 8. Sign the APK using apksigner (Standard Android Build Tool)
# Replace [keystore] with your .jks file path
apksigner sign --ks [my-release-key.jks] --out app-release-signed.apk app-release-unsigned.apk
```

## 6. Installation & Testing
1. Transfer the `app-debug.apk` or `app-release-signed.apk` to your **Huawei Y7 Prime**.
2. Enable **"Install from Unknown Sources"** in Android Settings.
3. Open the file and tap **Install**.

---
**Build Engineer Note:** 
Always run `npx cap copy android` after making small HTML/CSS changes to quickly update the native project without a full sync.