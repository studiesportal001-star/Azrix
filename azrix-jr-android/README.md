# Azrix Jr — Android app

A thin offline WebView shell around the Azrix Jr panel. The whole app is one
HTML file in `app/src/main/assets/index.html`; the Java class does nothing but
display it and handle the back button.

No `INTERNET` permission is declared, so the app cannot reach the network at
all. Everything you record stays in the WebView's local storage on the phone.

- Package: `com.azrix.jr`
- Min Android: 7.0 (API 24) · Target: Android 14 (API 34)
- Size: roughly 1–2 MB installed

---

## Three ways to get the APK

### 1. GitHub Actions (no tools to install)

1. Create a new GitHub repository.
2. Upload this whole folder to it and push to `main`.
3. Open the **Actions** tab. The *Build APK* workflow runs by itself.
4. When it finishes, download `azrix-jr-debug-apk` from the run's Artifacts.
5. Copy the `.apk` to your phone and open it. Android will ask you to allow
   installs from that source — that is expected for an app you built yourself.

### 2. Android Studio

1. **File → Open** and pick this folder.
2. Let it sync (it downloads Gradle and the SDK bits it needs).
3. **Build → Build Bundle(s) / APK(s) → Build APK(s)**.
4. The APK lands in `app/build/outputs/apk/debug/`.

To build one you can publish or keep long-term, use **Build → Generate Signed
Bundle / APK**, create a keystore, and keep that keystore file safe — Android
will refuse to update the app later if it is signed with a different key.

### 3. Command line

Needs JDK 17 and the Android SDK, with `ANDROID_HOME` set:

```bash
gradle wrapper          # first time only, creates ./gradlew
./gradlew assembleDebug
```

---

## Changing the app

The panel is entirely `app/src/main/assets/index.html`. Edit it, rebuild, done —
no Java changes needed for anything to do with features, layout or colours.

The launcher icons under `app/src/main/res/mipmap-*/` are generated from the
Azrix bolt on the brand navy (`#14262F`).

## Moving your existing records across

The phone app and the web version keep separate stores. To carry your data over:

1. In the web version: **Settings → Export a backup**, which gives you a `.json`.
2. Put that file somewhere you can open it on the phone and copy its contents.
3. In the app: **Settings → Restore from backup**, paste, restore.

The same route works in reverse, and is worth doing every so often regardless —
uninstalling the app clears its storage.

## A note on the screen lock

The code lock in Settings keeps the panel behind four to six digits if someone
picks up your unlocked phone. It is not encryption, and it will not stop anyone
with real access to the device. Treat it as a curtain, not a safe.
