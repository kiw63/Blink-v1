# Blink Browser for Android

Blink is a native Android browser app built on Android System WebView. It is not a website mock-up. The UI follows the supplied reference: deep black/navy surfaces, violet accents, rounded address/search controls, home shortcuts, tab manager, overflow menu, bookmarks, download manager, and settings.

## What is implemented in this source release

- Native Android app named **Blink** (Java + Android WebView).
- HTTP and HTTPS address navigation; domain-like input gets `https://`; other input is searched using Google, Bing, or Baidu.
- Link navigation inside the app, ordinary redirects, back/forward/reload, and best-effort `target=_blank` popup tabs.
- Multiple tabs and tab close/switch actions.
- Bookmark list stored on-device, add/delete/share actions.
- Normal browsing history stored on-device (up to 250 entries), open/delete/clear actions.
- Android DownloadManager for direct HTTP/HTTPS downloads, visible progress/status via Android's download service, open/share/cancel actions.
- File chooser support for websites that ask the user to upload a file.
- Dark/light appearance and a data-saving option that blocks remote images while enabled.
- Optional separate WebView profile for private tabs when supported by the device's System WebView. Private tabs are excluded from Blink's local history/session list.
- Security defaults: Android WebView Safe Browsing enabled, TLS certificate failures cancelled (never bypassed), mixed HTTP content blocked inside HTTPS pages, no JavaScript-to-native bridge, file URL access disabled, and private profiles isolated when the WebView provider supports multi-profile.

## Important limitations

1. **This source package is not a built APK.** The current authoring environment does not have the Android SDK/Gradle installed and cannot download build dependencies, so it could not compile or run the app on a device here. The project includes a GitHub Actions build workflow which can generate a debug APK once the source is placed in a GitHub repository and the workflow is run.
2. WebView is not a 100% replacement for full Chrome. Some sites require a newer System WebView, Google Play Services, browser-specific APIs, extensions, passkeys, DRM, or native apps. Multi-profile private tabs only work if the installed WebView provider supports the feature.
3. A browser cannot promise access to every URL. Dead sites, DNS/ISP/government blocks, geo-restrictions, certificate errors, site-side bot checks, and links requiring special native apps may still fail. Blink does not include a VPN, proxy service, or censorship-bypass server.
4. HTTP links are supported because requested, but HTTP is not encrypted. Prefer HTTPS whenever the site supports it.
5. **DDoS protection does not apply directly to a local browser APK** because the APK is not a public server. If Blink later operates a proxy/API/server, that server needs separate DDoS mitigation, rate limits, monitoring, secure hosting, and operational response. No software can honestly guarantee protection against every attacker.
6. All native controls in this project have actions wired, but an actual release still needs device testing, accessibility checks, download edge-case testing, and security review. Please do not treat the code as independently audited or production-certified.

## Build a debug APK with GitHub Actions

The included workflow is `.github/workflows/android-build.yml`. It uses Java 17, Gradle 8.13, Android SDK Platform 36, and Android Build Tools 36.0.0, then uploads `app-debug.apk` as a workflow artifact.

1. Create a new empty repository on GitHub.
2. Upload the **extracted project files and folders** into the repository root (not the ZIP as a single file), and commit them on the `main` branch.
3. Open the repository's **Actions** tab and run **Build Blink Android APK**. It also runs automatically after a push to `main`.
4. When the run completes successfully, open that run's **Artifacts** section and download `Blink-debug-apk`. Extract it to find `app-debug.apk`.
5. Move the APK to the Android phone, allow installation for the file manager/browser used to open it, and install it. The debug package name is `com.blink.browser.debug`.

A successful Actions build is still not the same as full-device QA; test on the target phone before relying on it.

## Build locally

Open this project in a recent Android Studio with JDK 17, Android SDK Platform 36 and Build Tools 36.0.0 installed. Use a local Gradle 8.13 installation (or let your IDE configure a compatible Gradle distribution) and run:

```bash
gradle --no-daemon assembleDebug
```

The output should be `app/build/outputs/apk/debug/app-debug.apk`.

## Package

- Package/application ID: `com.blink.browser.debug` for the debug build.
- App label: Blink.
- Minimum Android API: 26 (Android 8.0).
- Primary entry point: `app/src/main/java/com/blink/browser/MainActivity.java`.

## Ikon aplikasi Blink

Ikon launcher Blink sudah disiapkan pada resource `mipmap-*` untuk berbagai kepadatan layar dan adaptive icon Android 8+. Manifest menggunakan `@mipmap/ic_launcher`, sehingga ikon ini akan muncul pada launcher setelah APK berhasil dibangun dan dipasang. Bentuk akhirnya dapat sedikit berbeda tergantung launcher Android yang digunakan.
