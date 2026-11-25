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

## Implementation order
1. Apply SICA EXTERNAL branding and extracted visual assets; preserve upstream license notices.
2. Keep startup free of an access-key gate.
3. Map the quick-patch labels and dashboard onto the existing patch architecture. Do not claim any patch works until its format, target paths, and behavior are verified.
4. Adapt Spanish strings and other available localizations.
5. Test navigation, file operations, package import/export, cleaner, and wallpaper flows on supported simulator/device configurations.

## Safety, compatibility, licensing
- Device-level features depend on iOS build support and device permissions. Simulator success does not prove device-level access.
- Back up app data before applying file replacements or patches.
- Review GPL-3.0 and third-party notices before redistribution.
- Do not commit signing certificates, provisioning profiles, credentials, or personal data.
