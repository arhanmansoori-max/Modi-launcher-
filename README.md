# Modi Launcher — Android project

A native Kotlin + Jetpack Compose starter inspired by the supplied CrewCore screenshots.

## What currently works
- Home, Account, and Help tabs.
- Purple/red dark UI and responsive cards.
- Checks whether the official Among Us Android package (`com.innersloth.spacemafia`) is installed.
- Launches Among Us using Android's normal launch intent.
- Stores local picture-quality, frame-rate-preference, and guest-mode settings.
- Collects basic in-app diagnostic messages and shares them through Android's share sheet.
- Requests no special permissions.

## Explicit placeholders / limitations
- **This is not a CrewCore clone and does not contain CrewCore code.**
- **No actual mod menu is injected into Among Us.**
- The “Unlock frame rate” option is only a saved preference; it does not change the game's frame-rate cap.
- Picture quality is only a saved preference; it does not alter the game's rendering.
- Google and Discord sign-in are not implemented. Do not enter credentials into this app.
- The plugin system is an architectural next step only. This preview does not load or execute third-party plugin code.
- No server, account backend, automatic mod download/update, or game-version compatibility database is included.
- Package visibility and launching can vary by Android version and game installation source.

## Build an APK
Requirements:
- Android Studio (recommended) with Android SDK Platform 35 installed.
- JDK 17.
- Internet access during the first Gradle sync to download Gradle and Android dependencies.

1. Extract the ZIP.
2. Open the `ModiLauncher` folder in Android Studio.
3. Allow Gradle sync to finish.
4. Choose **Build > Build Bundle(s) / APK(s) > Build APK(s)**.
5. Install the debug APK on your Android 15 phone, or use **Run** with USB debugging enabled.

Command-line alternative from this folder:
`gradle assembleDebug`

The expected output is `app/build/outputs/apk/debug/app-debug.apk`.

## Safe plugin architecture roadmap
For a real modular system, define a versioned plugin manifest (id, display name, version, minimum launcher version, permissions/capabilities, and signature/hash), validate it, and keep plugins sandboxed or use Android-supported IPC. Do not load arbitrary downloaded DEX/native code into the launcher. Game modifications should use documented or explicitly authorized extension points and must remain compatible with the game's rules and security model.

## Package
`com.modilauncher.app`

## Version
`1.0.0` (starter project)


## Phone-only build option (cloud)
This repository includes `.github/workflows/android-build.yml` for a cloud build.

1. On your phone, sign in to GitHub and create a new repository named `ModiLauncher`.
2. Upload the extracted project files and folders to that repository. Make sure hidden folders such as `.github` are included; the GitHub website's upload flow may not make this convenient on mobile.
3. Open the repository's **Actions** tab and select **Build Modi Launcher APK**.
4. Tap **Run workflow** (or push to the `main` branch to trigger it).
5. When the workflow finishes successfully, open its run, find **Artifacts**, and download `modi-launcher-debug-apk`.
6. Extract the downloaded artifact ZIP; it contains `app-debug.apk`. Tap the APK to install it, allowing installs from that source only if Android asks.

Cloud builds require a GitHub account and a successful build run. The workflow is supplied but has not been executed or verified in this environment. Do not publish signing keys, passwords, or account tokens in the repository.
