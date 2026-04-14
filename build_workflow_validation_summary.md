# CIPS 2026 Revision Hub: Build Workflow Review & Validation

This document provides a final validation of the mobile build architecture to ensure 100% compatibility with Android 8.1 (API 27) on Snapdragon 450 devices.

---

## 1. Technical Baseline Validation
*   **Target Device:** Huawei Y7 Prime 2019 (Snapdragon 450, 3GB RAM).
*   **OS Version:** Android 8.1 (Oreo).
*   **Bridge Layer:** Capacitor v3 (Selected for superior legacy WebView support).

## 2. Configuration Audit

### ✅ Capacitor Config (`capacitor.config.json`)
*   **webDir:** Set to `www` (aligned with standard build outputs).
*   **androidScheme:** Forced to `https` to prevent "Mixed Content" blocks on older WebViews.
*   **Hardware Acceleration:** Enabled for smooth UI transitions on the Adreno 506 GPU.

### ✅ Gradle Settings (`variables.gradle`)
*   **minSdkVersion:** 21 (Lollipop).
*   **targetSdkVersion:** 27 (Oreo 8.1).
*   **compileSdkVersion:** 27.
*   **Dependency Pinning:** Essential AndroidX libraries are pinned to versions compatible with API 27 to prevent build-time crashes caused by modern library assumptions.

## 3. Automation Workflow (GitHub Actions)
The `build-apk.yml` is configured to:
1.  **JDK 11 Environment:** Required for Gradle 7+ compatibility while targeting older SDKs.
2.  **Web Asset Build:** Runs `npm run build` to generate the `dist/www` folder.
3.  **Capacitor Sync:** Executes `npx cap sync android` to bridge plugins.
4.  **Signing Logic:** Uses `KEYSTORE_FILE` secret to produce a release-ready, signed APK.

## 4. Performance Optimization Checklist
*   **[STRICT] No Backdrop Blur:** UI components are configured to use solid background colors or high-opacity overlays, as `backdrop-blur` causes significant lag on Snapdragon 450.
*   **[STRICT] WebP Only:** All new assets must be in `.webp` format to minimize memory footprint.
*   **[STRICT] Polyfills:** The `core-js` bundle is included in the base HTML to ensure modern JavaScript doesn't break the Android 8.1 WebView.

## 5. Deployment Commands (Refresher)
```bash
# Production Build Sequence
npm install
npm run build
npx cap copy android
npx cap sync android
cd android && ./gradlew assembleRelease
```

---
**Status:** Build Architecture Validated. The workflow is ready for the final release cycle.