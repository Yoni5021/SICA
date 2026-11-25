# SICA EXTERNAL — reconstruction plan

## Goal
Build a SICA EXTERNAL-branded derivative using this SwiftUI project and the observable inventory from the user's `EXTERNAL iOS NO KEY.ipa`.

The IPA contains a compiled SwiftUI executable, not original Swift source. Exact view code, layout constants, and all internal behavior cannot be automatically recovered. This plan maps observable resources and features onto the existing source.

## Startup
- Do not recreate the IPA's `AccessGateView`, `requiredAccessKey`, access-key prompt, or UNLOCK flow.
- Open the main interface directly.
- Keep first-run onboarding separate unless explicitly asked to remove it; language selection and compatibility guidance are not the lost access gate.
- Keep optional password protection for patch packages unless explicitly requested otherwise; it is separate from startup access.

## Observable identity and assets
- Original display identity: RYUMA EXTERNAL. Requested derivative: SICA EXTERNAL.
- Original bundle identifier: `com.apple.mobile.MobileHouseArrest`.
- Original version/build: 1.1.1 (7).
- Resources found: app icon, red/black technology background, brand avatar, button-click sound.
- Localizations found: Spanish, English, Arabic, Brazilian Portuguese, Vietnamese, Simplified Chinese.
- Seven quick-patch labels found: Aim Drag, Aim Neck, Antenna, 144 FPS, Aim Body, Aim Chest, Magic. Review the catalog and payload inventory before importing; this document does not recreate binary payloads.

## Feature map
| IPA feature | Existing source starting point |
|---|---|
| Dashboard/navigation | `ThreeOneOSFive/ContentView.swift`, `views/RepositoryHomeView.swift` |
| Patch library/editor | `views/PatchProjectsView.swift`, `views/PatchProjectEditorView.swift`, `helpers/PatchProjectStore.swift`, `PatchDraftService.swift` |
| Patch import/export | `helpers/PatchPackageCodec.swift`, `SecureZIPArchive.swift` |
| App/container browser | `views/AppDataBrowserView.swift`, `views/FileBrowserView.swift`, `helpers/ContainerBrowserLogic.swift` |
| File operations | `helpers/FileManagerService.swift`, `FileOperationCoordinator.swift`, `FileReplacementService.swift` |
| Cleaner | `views/CleanerView.swift`, `helpers/LimitedCleanerService.swift` |
| Wallpaper lab | `views/WallpaperLabView.swift`, `helpers/WallpaperLabService.swift` |
| Settings/language/logs | `views/SettingsView.swift`, `LogView.swift`, `helpers/Localization.swift` |
| Visual system | `views/DesignSystem.swift` |

## Utility behavior verified in source (not device-tested)
- Cleaner is intentionally scoped to each app container's `Library/Caches` and `tmp`; it validates the container root before scanning/removing contents. It is not a general-purpose system cleaner.
- Wallpaper Lab checks MHA-C2 container write access before installation, creates backups, and requires an explicit confirmation before applying a package. Actual installation depends on device permissions and supported iOS state.
- Patch Projects includes a separate optional package-unlock flow for protected project entries. This is not the startup access-key screen and remains intact.
- File browser supports multiple tabs, app-container navigation, search/sorting, import/export, copy/move/archive, and multi-select deletion. Destructive file deletion and import/transfer replacement conflicts use confirmation dialogs; actual visibility/access depends on MHA-C2 and iOS permissions.
- Patch library deletion now presents a destructive confirmation before removing one or multiple selected packages. Wallpaper-package deletion also presents a confirmation alert.
- A source-wide audit of all Swift files found no call site for `displayIdentityAttribution` or `DisplayAttributionSheet`; the five-second hidden-gesture helper remains present but unattached. Separate display-identity attestation code remains in `Utils.swift` and has not been altered.
- These are source-level findings only; no Xcode build or real-device test has been performed.

## Current reconstruction status
- [x] Set the app display name and primary navigation branding to SICA EXTERNAL.
- [x] Apply the SICA red/black visual accent system.
- [x] Point the in-app GitHub link, release-update checker, and attribution metadata to the SICA fork (update offers will remain empty until the fork publishes a release).
- [x] Update English, Vietnamese, and Simplified Chinese product-name strings while retaining the `.3105` package extension and format identifiers.
- [x] Add Spanish as an app language, register its strings in the Xcode project, and fall back to English for untranslated keys.
- [x] Translate all current English localization keys into Spanish, including dashboard, file browser, patch manager, repository, wallpaper, Gestalt, and system status; key parity audit passes with 654 keys and no duplicates.
- [x] Disable automatic kernel-exploit invocation at launch; device-level exploit code remains in the upstream-derived project and has not been validated here.
- [x] Keep the startup access-key gate out of the reconstruction; the optional patch-package key remains a separate feature.
- [ ] Replace the binary app icon and remaining original visual assets. The current asset catalog still contains the inherited icon; the original IPA's red/black background, avatar, and click sound have not yet been imported.
- [x] Finish visible SICA EXTERNAL labels in the log export, repository-source fallback labels, and log prefix; retain `3105` where it is a package extension, temporary-file prefix, or compatibility identifier.
- [x] Replace the in-app `AppLogo` rendering with a native SICA red-on-dark brand mark; the binary home-screen app icon is still pending.
- [ ] Finish the project-wide attribution/hidden-gesture call-site audit. The helper `DisplayIdentityAttribution.swift` contains a window-wide 5-second long-press that opens an attribution sheet; no attachment was found in the inspected app roots (`App.swift`, `ContentView.swift`, `RepositoryHomeView.swift`, `AppDataBrowserView.swift`, `SettingsView.swift`, or `OnboardingView.swift`).
- [x] Document source-level behavior and safety boundaries for Cleaner, Wallpaper Lab, protected patch projects, and file-browser tabs (not device-tested).
- [x] Add a destructive confirmation before patch-library package deletion, including multi-selection; reuse existing localized browser deletion prompts.
- [ ] Map only safe, verified utility features; do not import game aim-assist or cheat payloads.
- [ ] Build, test, and sign with Xcode on macOS. The repository currently has no automated test target or published SICA release.

## Implementation order
1. Replace the binary home-screen app icon and remaining IPA visual assets; preserve upstream license notices. The in-app brand mark is complete, and the source-wide hidden-attribution audit and visible-branding cleanup are complete.
2. Keep startup free of an access-key gate.
3. Map safe dashboard and utility features onto the existing architecture. Do not claim any patch works until its format, target paths, and behavior are verified.
4. Adapt remaining available localizations; Spanish key parity is complete.
5. Test navigation, file operations, package import/export, cleaner, and wallpaper flows on supported simulator/device configurations.

## Safety, compatibility, licensing
- Device-level features depend on iOS build support and device permissions. Simulator success does not prove device-level access.
- Back up app data before applying file replacements or patches.
- Review GPL-3.0 and third-party notices before redistribution.
- Do not commit signing certificates, provisioning profiles, credentials, or personal data.
