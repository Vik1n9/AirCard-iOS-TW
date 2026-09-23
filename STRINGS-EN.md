# AirCard-iOS — English UI string inventory (for zh-Hant)

**Source of truth:** [Mak5er/AirCard-iOS](https://github.com/Mak5er/AirCard-iOS) `main` (shallow clone at `/workspace/AirCard-iOS-upstream`).

**Not a source of truth for wording:** [SheldonJoO/AirCard-iOS-CN](https://github.com/SheldonJoO/AirCard-iOS-CN) — used only as a *file map* of what they hardcoded.

**Translator:** Trotsky fills `zh-Hant` column. Do **not** invent Traditional Chinese here.

## Counts

| Category | Count |
|---|---:|
| UI chrome (Text/Label/Button/Section/nav/alert/dialog/field/link/picker/…) | 194 |
| Runtime status / errors / activity-log lines shown in UI | 73 |
| Enum display rawValues (tabs, pickers, modes) | 28 |
| Info.plist user-visible strings | 10 |
| **Total app strings** | **305** |
| README headed sections/blocks | 17 |

## Must stay English / keep tokens

From CN README (reference policy, apply to zh-Hant fork too):

- **App display name `AirCard-iOS`** must stay exactly that — it is the Bonjour pairing service name shown in Settings › Privacy & Security › Developer Mode › **Pair with AirCard-iOS**. Renaming breaks the system pairing entry.
- **Bundle ID / service identifiers** stay unchanged (CN did not change logic, paths, Bundle ID, pairing service name).
- Keep product/tech tokens as-is inside translated sentences where useful: `LocalDevVPN`, `NeoSpring`, `PosterBoard`, `airlift` / `AirliftFFI`, `.passthm`, `.tendies`, `TelephonyUI-*`, handles `@mak5er` / `@merybist`, `GitHub`, file names like `aircard_pairing.plist`.
- IP examples (`10.7.0.1`, `127.0.0.1`) stay as-is.

## CN fork file map (reference only)

CN hardcoded Simplified into these paths (no `.lproj` / `.xcstrings`):

- `ios-app/AirCardApp.swift`
- `ios-app/AppViewModel.swift`
- `ios-app/ContentView.swift`
- `ios-app/Info.plist`
- `ios-app/Models.swift`
- `ios-app/NetworkStatus.swift`
- `ios-app/PairingController.swift`
- `ios-app/RespringHelper.swift`
- `ios-app/TendiesEngine.swift`
- `ios-app/TendiesModel.swift`
- `ios-app/TendiesView.swift`
- `ios-app/Utilities.swift`
- `README.md`

CN touched the same Swift UI surfaces as upstream (`ContentView`, `TendiesView`, `AppViewModel`, `Models`, `PairingController`, `TendiesEngine`, `Info.plist`, `README`) plus comment-level edits in helpers. Upstream has **no** `.lproj` / String Catalog either.

## Approach note (for parent)

CN pattern: **hardcode** translated literals directly in Swift (and README), no String Catalog.

**Recommendation:** Mirror that for zh-Hant parity with CN (fast, same merge surface, no Xcode localization plumbing). Adding `Localizable.xcstrings` would be cleaner long-term but is *not* trivial here — strings are scattered across Views + ViewModel status/`errorMessage`/`log.append` + enum `rawValue`s + Info.plist — Catalog would need systematic `String(localized:)` / `Text("key")` refactors beyond a drop-in file. Parent decides; inventory assumes hardcode-mirror.

---

## App UI & runtime strings

Fill `zh-Hant` leaving technical tokens noted above in English. For ternary / nil-coalescing rows, translate the full template including both branches / defaults (defaults are also listed as separate rows where extracted).

### `ios-app/AppViewModel.swift`

| id | line | kind | English (exact) | zh-Hant | notes |
|---|---:|---|---|---|---|
| `vm.pairing-file-loaded` | 206 | pairingStatus | `Pairing file loaded ✅ (\(originalName ?? "aircard_pairing.plist"))` |  | fixed full string with nested ?? quotes |
| `vm.pairing-file-loaded-default` | 206 | pairingStatus | `aircard_pairing.plist` |  | nil-coalescing default inside vm.pairing-file-loaded; KEEP filename |
| `vm.failed-to-save-pairing-file-n` | 209 | errorMessage | `Failed to save pairing file: \(error.localizedDescription)` |  | UI-bound errorMessage |
| `vm.starting-local-host` | 245 | pairingStatus | `Starting local host…` |  | UI-bound pairingStatus |
| `vm.paired-successfully` | 256 | pairingStatus | `Paired successfully! ✅` |  | UI-bound pairingStatus |
| `vm.pairing-complete-n` | 257 | activityLog | `Pairing complete: \(path)` |  | visible in Activity/Flash Log |
| `vm.cancelled` | 261 | pairingStatus | `Cancelled.` |  | UI-bound pairingStatus |
| `vm.pairing-failed-n` | 265 | errorMessage | `Pairing failed: \(error.localizedDescription)` |  | UI-bound errorMessage |
| `vm.pairing-file-deleted` | 293 | pairingStatus | `Pairing file deleted` |  | UI-bound pairingStatus |
| `vm.pairing-file-is-required-before-scanning-pair-this-ipho` | 344 | errorMessage | `Pairing file is required before scanning. Pair this iPhone or select a .plist first.` |  | UI-bound errorMessage |
| `vm.open-apple-pay-double-click-side-button-and-tap-your-ca` | 352 | scanStatusText | `Open Apple Pay (double-click Side button) and tap your card…` |  | UI-bound scanStatusText |
| `vm.started-live-card-scanner` | 354 | activityLog | `Started live card scanner…` |  | visible in Activity/Flash Log |
| `vm.scanner-stopped-n` | 393 | scanStatusText | `Scanner stopped: \(msg)` |  | UI-bound scanStatusText |
| `vm.scanner-error-n` | 394 | activityLog | `❌ Scanner error: \(msg)` |  | visible in Activity/Flash Log |
| `vm.card-scanner-error-n` | 395 | errorMessage | `Card scanner error: \(msg)` |  | UI-bound errorMessage |
| `vm.scanning-stopped-total-cards-n` | 397 | scanStatusText | `Scanning stopped. Total cards: \(vm.cards.count).` |  | UI-bound scanStatusText |
| `vm.scanning-stopped-total-cards-n-2` | 398 | activityLog | `Scanning stopped. Total cards: \(vm.cards.count).` |  | visible in Activity/Flash Log |
| `vm.scanning-stopped-total-cards-n-3` | 414 | scanStatusText | `Scanning stopped. Total cards: \(cards.count).` |  | UI-bound scanStatusText |
| `vm.found-card-n` | 460 | scanStatusText | `Found card: \(candidate)` |  | UI-bound scanStatusText |
| `vm.found-card-n-2` | 461 | activityLog | `Found card: \(candidate)` |  | visible in Activity/Flash Log |
| `vm.notice-loopback-vpn-not-detected-attempting-direct-loop` | 611 | activityLog | `⚠️ Notice: Loopback VPN not detected, attempting direct loopback (127.0.0.1)...` |  | visible in Activity/Flash Log |
| `vm.n-n-flashing-card-n` | 625 | activityLog | `[\(i+1)/\(selected.count)] Flashing card \(cleanId.prefix(12))…` |  | visible in Activity/Flash Log |
| `vm.no-image-for-card-n` | 638 | activityLog | `  ⚠️ No image for card \(cleanId.prefix(8))` |  | visible in Activity/Flash Log |
| `vm.failed-to-generate-card-skins` | 645 | activityLog | `  ⚠️ Failed to generate card skins` |  | visible in Activity/Flash Log |
| `vm.injecting-skins-into-n-pkpass` | 660 | activityLog | `  ⚡ Injecting skins into \(cleanId.prefix(10)).pkpass…` |  | visible in Activity/Flash Log |
| `vm.failed-write-card-skins` | 692 | activityLog | `  ❌ Failed to write card skins: \(errDesc ?? "exploit error")` |  | fixed full string with nested ?? quotes |
| `vm.failed-write-card-skins-default` | 692 | activityLog | `exploit error` |  | nil-coalescing default inside vm.failed-write-card-skins |
| `vm.skins-applied-invalidating-pass-cache` | 698 | activityLog | `  ✅ Skins applied! Invalidating pass cache…` |  | visible in Activity/Flash Log |
| `vm.pass-cache-invalidated` | 730 | activityLog | `  ✅ Pass cache invalidated` |  | visible in Activity/Flash Log |
| `vm.n-n-card-s-flashed-force-close-wallet-app-to-see-change` | 739 | activityLog | `🎉 \(successCount)/\(selected.count) card(s) flashed! Force-close Wallet app to see changes.` |  | visible in Activity/Flash Log |
| `vm.skins-successfully-applied-to-n-card-s-n-to-see-your-ne` | 740 | successAlertMessage | `Skins successfully applied to \(successCount) card(s)!\n\nPlease force-close the Wallet app on your iPhone (or reboot) to see your new designs.` |  | UI-bound successAlertMessage |
| `vm.card-flash-failed-check-connection-and-try-again` | 744 | activityLog | `❌ Card flash failed. Check connection and try again.` |  | visible in Activity/Flash Log |
| `vm.failed-to-read-passthm-invalid-or-unsupported-format` | 831 | errorMessage | `Failed to read .passthm — invalid or unsupported format.` |  | UI-bound errorMessage |
| `vm.no-key-images-loaded` | 880 | errorMessage | `No key images loaded.` |  | UI-bound errorMessage |
| `vm.notice-loopback-vpn-not-detected-attempting-direct-loop-2` | 890 | activityLog | `⚠️ Notice: Loopback VPN not detected, attempting direct loopback (127.0.0.1)...` |  | visible in Activity/Flash Log |
| `vm.staged-theme-assets-n-langs-joined-separator` | 977 | activityLog | `⚡ Staged theme assets (\(targetVer) · \(langs.joined(separator: ` |  | visible in Activity/Flash Log |
| `vm.writing-to-n` | 1000 | activityLog | `  Writing to \(targetName)…` |  | visible in Activity/Flash Log |
| `vm.write-to-n-failed` | 1030 | activityLog | `  ⚠️ Write to \(targetName) failed: \(lastErr ?? "error")` |  | fixed full string with nested ?? quotes |
| `vm.write-to-n-failed-default` | 1030 | activityLog | `error` |  | nil-coalescing default inside vm.write-to-n-failed |
| `vm.injected-into-n` | 1034 | activityLog | `  ✅ Injected into \(targetName)` |  | visible in Activity/Flash Log |
| `vm.passcode-theme-applied-lock-your-iphone-to-see-it` | 1049 | activityLog | `🎉 Passcode theme applied! Lock your iPhone to see it.` |  | visible in Activity/Flash Log |
| `vm.passcode-theme-successfully-applied-n-to-see-your-new-p` | 1050 | successAlertMessage | `Passcode theme successfully applied!\n\nLock your iPhone (or restart) to see your new passcode keypad.` |  | UI-bound successAlertMessage |
| `vm.one-or-more-theme-injections-failed` | 1054 | activityLog | `❌ One or more theme injections failed.` |  | visible in Activity/Flash Log |
| `vm.please-configure-at-least-one-key-before-exporting` | 1063 | errorMessage | `Please configure at least one key before exporting.` |  | UI-bound errorMessage |
| `vm.failed-to-export-theme-n` | 1080 | errorMessage | `Failed to export theme: \(error.localizedDescription)` |  | UI-bound errorMessage |
| `vm.failed-to-import-n-n` | 1139 | errorMessage | `Failed to import \(url.lastPathComponent): \(error.localizedDescription)` |  | UI-bound errorMessage |
| `vm.no-pairing-file-active-pair-your-device-first-in-the-pa` | 1156 | errorMessage | `No pairing file active. Pair your device first in the Pairing tab.` |  | UI-bound errorMessage |
| `vm.auto-detect-failed-n-nensure-localdevvpn-is-connected-a` | 1176 | errorMessage | `Auto-detect failed: \(error.localizedDescription)\nEnsure LocalDevVPN is connected and device is unlocked.` |  | UI-bound errorMessage; KEEP product name LocalDevVPN |
| `vm.no-wallpapers-selected-to-flash` | 1185 | errorMessage | `No wallpapers selected to flash.` |  | UI-bound errorMessage |
| `vm.no-pairing-file-active-please-pair-your-device-first` | 1191 | errorMessage | `No pairing file active. Please pair your device first.` |  | UI-bound errorMessage |
| `vm.posterboard-container-could-not-be-found-automatically-` | 1202 | errorMessage | `PosterBoard container could not be found automatically. Ensure LocalDevVPN is connected and iPhone is unlocked.` |  | UI-bound errorMessage; KEEP product name LocalDevVPN |
| `vm.wallpapers-applied-successfully` | 1230 | activityLog | `🎉 Wallpapers applied successfully!` |  | visible in Activity/Flash Log |
| `vm.triggering-neospring-respring` | 1231 | activityLog | `⚡ Triggering NeoSpring respring...` |  | visible in Activity/Flash Log |
| `vm.error-n` | 1238 | activityLog | `❌ Error: \(error.localizedDescription)` |  | visible in Activity/Flash Log |
| `vm.triggering-neospring-respring-2` | 1244 | activityLog | `⚡ Triggering NeoSpring respring...` |  | visible in Activity/Flash Log |

### `ios-app/ContentView.swift`

| id | line | kind | English (exact) | zh-Hant | notes |
|---|---:|---|---|---|---|
| `ui.aircard-ios` | 42 | Text | `AirCard-iOS` |  | KEEP TOKEN `AirCard-iOS` (Bonjour/pairing display name; CN README) |
| `ui.apple-wallet-skins-passcode-themes-for-ios-18` | 45 | Text | `Apple Wallet Skins & Passcode Themes for iOS 18+` |  |  |
| `ui.lead-core-developer` | 58 | Label | `Lead & Core Developer` |  |  |
| `ui.chief` | 62 | Text | `Chief` |  |  |
| `ui.mak5er` | 72 | Text | `@mak5er` |  | KEEP proper noun / handle; KEEP proper noun/handle |
| `ui.https-github-com-mak5er` | 77 | Link | `https://github.com/mak5er` |  |  |
| `ui.github` | 80 | Text | `GitHub` |  | KEEP proper noun / handle; KEEP proper noun/handle |
| `ui.https-x-com-mak5er` | 87 | Link | `https://x.com/mak5er` |  |  |
| `ui.twitter-x` | 90 | Text | `Twitter / X` |  | KEEP proper noun / handle; KEEP proper noun/handle |
| `ui.base-ipa-developer` | 105 | Label | `Base IPA Developer` |  |  |
| `ui.base` | 109 | Text | `Base` |  |  |
| `ui.merybist` | 119 | Text | `@merybist` |  | KEEP proper noun / handle; KEEP proper noun/handle |
| `ui.https-github-com-merybist` | 124 | Link | `https://github.com/merybist` |  |  |
| `ui.github-2` | 127 | Text | `GitHub` |  | KEEP proper noun / handle; KEEP proper noun/handle |
| `ui.https-x-com-merybist` | 134 | Link | `https://x.com/merybist` |  |  |
| `ui.twitter-x-2` | 137 | Text | `Twitter / X` |  | KEEP proper noun / handle; KEEP proper noun/handle |
| `ui.core-exploit` | 156 | Text | `Core Exploit` |  |  |
| `ui.airlift-airtraffic-sync-sandbox-escape` | 158 | Text | `airlift (AirTraffic sync sandbox escape)` |  |  |
| `ui.passcode-themes` | 171 | Text | `Passcode Themes` |  |  |
| `ui.neospring-posterboard` | 186 | Text | `NeoSpring & PosterBoard` |  |  |
| `ui.springboard-reload-tendies-wallpapers-neonmodder123-ska` | 188 | Text | `SpringBoard reload & .tendies wallpapers (@neonmodder123, @skadz108, @rooootdev)` |  |  |
| `ui.credits` | 204 | navigationTitle | `Credits` |  |  |
| `ui.done` | 208 | Button | `Done` |  |  |
| `ui.copied` | 262 | Text | `Copied` |  | CompactLogView after copy |
| `ui.pairing` | 358 | Label | `Pairing` |  |  |
| `ui.wallet-cards` | 362 | Label | `Wallet Cards` |  |  |
| `ui.passcode` | 366 | Label | `Passcode` |  |  |
| `ui.wallpapers` | 370 | Label | `Wallpapers` |  |  |
| `ui.notice` | 373 | alert | `Notice` |  |  |
| `ui.ok` | 377 | Button | `OK` |  |  |
| `ui.success` | 381 | alert | `Success! 🎉` |  |  |
| `ui.ok-2` | 382 | Button | `OK` |  |  |
| `ui.aircard-ios-2` | 415 | Text | `AirCard-iOS` |  | KEEP TOKEN `AirCard-iOS` (Bonjour/pairing display name; CN README) |
| `ui.ios-n-v1-3` | 418 | Text | `iOS \(ProcessInfo.processInfo.operatingSystemVersion.majorVersion) · v1.3` |  |  |
| `ui.apply-custom-wallet-card-skins-and-passcode-themes-on-d` | 425 | Text | `Apply custom wallet card skins and passcode themes on-device using the AirTraffic sandbox escape.` |  |  |
| `ui.network` | 433 | Section | `Network` |  |  |
| `ui.active-pairing` | 438 | Section | `Active Pairing` |  |  |
| `ui.ready-to-exploit` | 443 | Text | `Ready to exploit ✅` |  |  |
| `ui.n-n` | 445 | Text | `\(vm.pairingFileName) (\(vm.pairingFileSizeString))` |  |  |
| `ui.not-paired` | 452 | Text | `Not Paired` |  |  |
| `ui.tap-pair-this-iphone-below-to-pair` | 454 | Text | `Tap 'Pair This iPhone' below to pair.` |  |  |
| `ui.delete-pairing-session` | 472 | confirmationDialog | `Delete pairing session?` |  |  |
| `ui.delete` | 476 | Button | `Delete` |  |  |
| `ui.cancel` | 477 | Button | `Cancel` |  |  |
| `ui.delete-pairing-message` | 479 | Text | `The active pairing credentials will be removed.` |  | confirmationDialog message |
| `ui.pair-on-this-iphone` | 483 | Section | `Pair on This iPhone` |  |  |
| `ui.starting-local-pairing-host` | 488 | Text | `Starting local pairing host…` |  |  |
| `ui.enter-this-pin-on-this-iphone` | 495 | Text | `ENTER THIS PIN ON THIS IPHONE:` |  |  |
| `ui.copy-2` | 508 | Label | `Copy` |  |  |
| `ui.settings-privacy-security-developer-mode-pair-with-airc` | 515 | Text | `Settings › Privacy & Security › Developer Mode › Pair with AirCard-iOS` |  | KEEP substring `AirCard-iOS` in path (system Settings label) |
| `ui.open-settings-app-now` | 524 | Label | `Open Settings App Now` |  |  |
| `ui.cancel-pairing` | 542 | Text | `Cancel Pairing` |  |  |
| `ui.pair-this-iphone` | 573 | Text | `Pair This iPhone` |  |  |
| `ui.re-pair-this-iphone` | 573 | Text | `Re-Pair This iPhone` |  |  |
| `ui.activity-log-n-lines` | 589 | disclosureTitle | `Activity Log (\(vm.log.count) lines)` |  |  |
| `ui.aircard-ios-3` | 599 | navigationTitle | `AirCard-iOS` |  | KEEP TOKEN `AirCard-iOS` (Bonjour/pairing display name; CN README) |
| `ui.credits-2` | 609 | Text | `Credits` |  |  |
| `ui.loopback-vpn-active` | 649 | Text | `Loopback VPN Active` |  |  |
| `ui.loopback-vpn-not-detected` | 649 | Text | `Loopback VPN Not Detected` |  |  |
| `ui.rsd-tunnel-ready` | 652 | Text | `RSD tunnel ready — exploit will connect.` |  |  |
| `ui.connect-localdevvpn-before-flashes` | 653 | Text | `Connect LocalDevVPN before running flashes.` |  | KEEP product name LocalDevVPN |
| `ui.setup-localdevvpn` | 661 | Text | `Setup LocalDevVPN:` |  | KEEP product name LocalDevVPN |
| `ui.1-open-localdevvpn-app-and-tap-connect` | 664 | instructionStep | `1. Open LocalDevVPN app and tap Connect.` |  | VPN/setup instruction step; KEEP product name LocalDevVPN |
| `ui.2-return-to-aircard-ios-status-indicator-turns-green` | 665 | instructionStep | `2. Return to AirCard-iOS — status indicator turns green.` |  | VPN/setup instruction step |
| `ui.launch-localdevvpn` | 671 | Link | `Launch LocalDevVPN` |  | KEEP product name LocalDevVPN |
| `ui.device-ip` | 681 | Text | `Device IP:` |  |  |
| `ui.assign-card-skin` | 804 | Text | `Assign Card Skin` |  |  |
| `ui.tap-to-choose-photo` | 808 | Text | `Tap to choose photo` |  |  |
| `ui.card-n` | 830 | Text | `Card #\(cardIndex + 1)` |  |  |
| `ui.wallet-cards-n` | 931 | navigationTitle | `Wallet Cards (\(vm.cards.count))` |  |  |
| `ui.scan-cards` | 939 | Text | `Scan Cards` |  |  |
| `ui.stop-scan` | 939 | Text | `Stop Scan` |  |  |
| `ui.add-card-manually` | 951 | Label | `Add Card Manually` |  |  |
| `ui.set-skin-for-all-cards` | 958 | Label | `Set Skin for All Cards...` |  |  |
| `ui.select-all` | 966 | Label | `Select All` |  |  |
| `ui.deselect-all` | 972 | Label | `Deselect All` |  |  |
| `ui.clear-all-cards` | 982 | Label | `Clear All Cards` |  |  |
| `ui.credits-3` | 990 | Label | `Credits` |  |  |
| `ui.choose-image-source` | 1013 | confirmationDialog | `Choose Image Source` |  |  |
| `ui.photo-library` | 1017 | Label | `Photo Library` |  |  |
| `ui.choose-from-files` | 1022 | Label | `Choose from Files…` |  |  |
| `ui.cancel-2` | 1024 | Button | `Cancel` |  |  |
| `ui.live-scanner-active` | 1086 | Text | `Live Scanner Active` |  |  |
| `ui.scanner-status` | 1092 | Text | `Scanner Status` |  |  |
| `ui.stop` | 1098 | Button | `Stop` |  |  |
| `ui.flash-log-n-lines` | 1149 | disclosureTitle | `Flash Log (\(vm.cardFlashLog.count) lines)` |  |  |
| `ui.flashing` | 1169 | Text | `Flashing…` |  |  |
| `ui.retry` | 1174 | Text | `Retry` |  |  |
| `ui.flash` | 1179 | Text | `Flash` |  |  |
| `ui.no-cards-detected-yet` | 1203 | Text | `No Cards Detected Yet` |  |  |
| `ui.tap-scan-cards-in-the-toolbar-above` | 1211 | Text | `Tap **Scan Cards** in the toolbar above.` |  |  |
| `ui.on-this-iphone-double-click-the-side-button-apple-pay-a` | 1217 | Text | `On this iPhone, **double-click the Side button** (Apple Pay), authenticate with **Face ID**, and **tap your card**.` |  |  |
| `ui.your-card-will-appear-here-automatically` | 1223 | Text | `Your card will appear here automatically!` |  |  |
| `ui.scan-cards-2` | 1240 | Text | `Scan Cards` |  |  |
| `ui.stop-scan-2` | 1240 | Text | `Stop Scan` |  |  |
| `ui.add-manually` | 1257 | Text | `Add Manually` |  |  |
| `ui.card-hash` | 1285 | Section | `Card Hash` |  |  |
| `ui.paste-card-hash-e-g-m6ndwzrkybfl` | 1286 | TextField | `Paste card hash (e.g. M6nDwZrkYbFl…)` |  |  |
| `ui.you-can-add-multiple-hashes-at-once-separate-them-with-` | 1293 | Text | `You can add multiple hashes at once — separate them with spaces, commas, or newlines.` |  |  |
| `ui.add-card` | 1298 | navigationTitle | `Add Card` |  |  |
| `ui.cancel-3` | 1302 | Button | `Cancel` |  |  |
| `ui.add` | 1305 | Button | `Add` |  |  |
| `ui.mode` | 1325 | Picker | `Mode` |  | Picker label (segmented Apply/Create) |
| `ui.flash-log-n-lines-2` | 1343 | disclosureTitle | `Flash Log (\(vm.passthmFlashLog.count) lines)` |  |  |
| `ui.passcode-theme` | 1353 | navigationTitle | `Passcode Theme` |  |  |
| `ui.themes-in-app-folder-on-my-iphone-aircard-ios` | 1381 | Section | `Themes in App Folder (On My iPhone › AirCard-iOS)` |  | KEEP substring AirCard-iOS |
| `ui.load` | 1389 | Button | `Load` |  |  |
| `ui.browse-files` | 1400 | Section | `Browse Files` |  |  |
| `ui.change-passthm` | 1405 | Label | `Change .passthm…` |  |  |
| `ui.choose-passthm-from-files` | 1405 | Label | `Choose .passthm from Files…` |  |  |
| `ui.clear` | 1414 | Text | `Clear` |  |  |
| `ui.interactive-lock-screen-preview` | 1433 | Section | `Interactive Lock Screen Preview` |  |  |
| `ui.theme-information` | 1439 | Section | `Theme Information` |  |  |
| `ui.files-in-theme` | 1440 | LabeledContent | `Files in theme` |  |  |
| `ui.digits-styled` | 1441 | LabeledContent | `Digits styled` |  |  |
| `ui.n-keys` | 1441 | LabeledContentValue | `\(theme.keysPreview.count) keys` |  | value template next to Digits styled |
| `ui.edit-in-theme-creator` | 1446 | Label | `Edit in Theme Creator` |  |  |
| `ui.remove-unload-theme` | 1464 | Text | `Remove / Unload Theme` |  |  |
| `ui.flashing-theme` | 1485 | Text | `Flashing Theme…` |  |  |
| `ui.retry-flash-theme` | 1497 | Text | `Retry Flash Theme` |  |  |
| `ui.flash-theme-to-iphone` | 1514 | Text | `Flash Theme to iPhone` |  |  |
| `ui.flash-language-target` | 1539 | Text | `Flash & Language Target` |  |  |
| `ui.system-caches` | 1545 | Text | `System Caches` |  |  |
| `ui.telephonyui-10-ios-18` | 1549 | Text | `TelephonyUI-10 (iOS 18+)` |  | KEEP cache folder name TelephonyUI-N; translate parenthetical only if desired |
| `ui.telephonyui-9-ios-16-17` | 1550 | Text | `TelephonyUI-9 (iOS 16–17)` |  | KEEP cache folder name TelephonyUI-N; translate parenthetical only if desired |
| `ui.telephonyui-8-ios-14-15` | 1551 | Text | `TelephonyUI-8 (iOS 14–15)` |  | KEEP cache folder name TelephonyUI-N; translate parenthetical only if desired |
| `ui.universal-all` | 1552 | Text | `Universal (All)` |  |  |
| `ui.system-language` | 1562 | Text | `System Language` |  |  |
| `ui.font-weight-style` | 1578 | Text | `Font Weight / Style` |  |  |
| `ui.universal-mode-flashes-600-files-for-all-languages-bold` | 1598 | Text | `Universal mode flashes ~600 files for all languages & Bold text. Selecting a specific language (e.g. Ukrainian) speeds up flashing dramatically.` |  |  |
| `ui.fast-mode-selected-only-targets-n-with-n` | 1603 | Text | `Fast mode selected: only targets \(vm.passcodeLanguageTarget.rawValue) with \(vm.passcodeBoldTarget.rawValue).` |  |  |
| `ui.slice-mode` | 1631 | Section | `Slice Mode` |  |  |
| `ui.interactive-lock-screen-preview-2` | 1647 | Section | `Interactive Lock Screen Preview` |  |  |
| `ui.export-passthm` | 1667 | Text | `Export .passthm...` |  |  |
| `ui.clear-all` | 1682 | Text | `Clear All` |  |  |
| `ui.poster-image` | 1699 | Section | `Poster Image` |  |  |
| `ui.change-photo` | 1703 | Label | `Change Photo…` |  |  |
| `ui.select-photo-for-keypad` | 1703 | Label | `Select Photo for Keypad…` |  |  |
| `ui.choose-poster-image-source` | 1708 | confirmationDialog | `Choose Poster Image Source` |  |  |
| `ui.photo-library-2` | 1712 | Label | `Photo Library` |  |  |
| `ui.choose-from-files-2` | 1717 | Label | `Choose from Files…` |  |  |
| `ui.cancel-4` | 1719 | Button | `Cancel` |  |  |
| `ui.slicing-style` | 1750 | Section | `Slicing Style` |  |  |
| `ui.seamless-poster` | 1753 | Text | `Seamless Poster` |  |  |
| `ui.circle-buttons` | 1754 | Text | `Circle Buttons` |  |  |
| `ui.artwork-is-clipped-into-individual-circular-button-icon` | 1761 | Text | `Artwork is clipped into individual circular button icons.` |  |  |
| `ui.seamless-artwork-spans-across-dialer-keys-without-circu` | 1761 | Text | `Seamless artwork spans across dialer keys without circular cuts (Adobe Dog style).` |  |  |
| `ui.zoom-framing` | 1772 | Text | `Zoom & Framing` |  |  |
| `ui.reset-position` | 1776 | Button | `Reset Position` |  |  |
| `ui.1fx` | 1799 | Text | `%.1fx` |  |  |
| `ui.drag-anywhere-on-the-dialer-preview-to-reposition` | 1808 | Text | `Drag anywhere on the dialer preview to reposition` |  |  |
| `ui.individual-keys` | 1820 | Section | `Individual Keys` |  |  |
| `ui.tap-a-button-row-to-assign-a-custom-image` | 1821 | Text | `Tap a button row to assign a custom image.` |  |  |
| `ui.key-n` | 1844 | Text | `Key \(btn.digit)` |  |  |
| `ui.choose-key-n-image-source-default` | 1877 | confirmationDialog | `` |  | nil-coalescing default inside ui.choose-key-n-image-source |
| `ui.choose-key-n-image-source` | 1877 | confirmationDialog | `Choose Key \(selectedDigitForPicker ?? "") Image Source` |  | fixed full string with nested ?? quotes |
| `ui.photo-library-3` | 1881 | Label | `Photo Library` |  |  |
| `ui.choose-from-files-3` | 1886 | Label | `Choose from Files…` |  |  |
| `ui.cancel-5` | 1888 | Button | `Cancel` |  |  |
| `ui.flashing-theme-2` | 1937 | Text | `Flashing Theme…` |  |  |
| `ui.retry-flash-theme-2` | 1949 | Text | `Retry Flash Theme` |  |  |
| `ui.flash-theme-to-iphone-2` | 1966 | Text | `Flash Theme to iPhone` |  |  |
| `ui.drag-preview-to-reposition` | 2080 | Text | `Drag preview to reposition` |  |  |

### `ios-app/Info.plist`

| id | line | kind | English (exact) | zh-Hant | notes |
|---|---:|---|---|---|---|
| `plist.aircard-ios` | 8 | Info.plist | `AirCard-iOS` |  | KEEP ENGLISH — display/pairing service name (CN README); KEEP TOKEN `AirCard-iOS` (Bonjour/pairing display name; CN README) |
| `plist.aircard-ios-advertises-an-on-device-pairing-service-so-` | 38 | Info.plist | `AirCard-iOS advertises an on-device pairing service so this iPhone can pair with itself, and connects to the local lockdown daemon to run the exploit.` |  | Info.plist user-visible; KEEP TOKEN `AirCard-iOS` (Bonjour/pairing display name; CN README) |
| `plist.aircard-ios-needs-photo-access-to-apply-custom-card-ski` | 40 | Info.plist | `AirCard-iOS needs photo access to apply custom card skins and passcode themes.` |  | Info.plist user-visible; KEEP TOKEN `AirCard-iOS` (Bonjour/pairing display name; CN README) |
| `plist.passcode-theme` | 62 | Info.plist | `Passcode Theme` |  | Info.plist user-visible |
| `plist.pairing-file` | 74 | Info.plist | `Pairing File` |  | Info.plist user-visible |
| `plist.posterboard-wallpaper` | 86 | Info.plist | `PosterBoard Wallpaper` |  | Info.plist user-visible |
| `plist.passcode-theme-archive` | 103 | Info.plist | `Passcode Theme Archive` |  | Info.plist user-visible |
| `plist.posterboard-wallpaper-archive` | 121 | Info.plist | `PosterBoard Wallpaper Archive` |  | Info.plist user-visible |
| `plist.posterboard-wallpaper-archive-2` | 143 | Info.plist | `PosterBoard Wallpaper Archive` |  | Info.plist user-visible |
| `plist.passcode-theme-archive-2` | 162 | Info.plist | `Passcode Theme Archive` |  | Info.plist user-visible |

### `ios-app/Models.swift`

| id | line | kind | English (exact) | zh-Hant | notes |
|---|---:|---|---|---|---|
| `model.pairing` | 52 | enumDisplay | `Pairing` |  | enum case pairing rawValue shown in pickers/tabs |
| `model.wallet-cards` | 53 | enumDisplay | `Wallet Cards` |  | enum case walletCards rawValue shown in pickers/tabs |
| `model.passcode` | 54 | enumDisplay | `Passcode` |  | enum case passcodeThemes rawValue shown in pickers/tabs |
| `model.wallpapers` | 55 | enumDisplay | `Wallpapers` |  | enum case wallpapers rawValue shown in pickers/tabs |
| `model.apply-passthm` | 69 | enumDisplay | `Apply .passthm` |  | enum case applyTheme rawValue shown in pickers/tabs |
| `model.create-theme` | 70 | enumDisplay | `Create Theme` |  | enum case themeCreator rawValue shown in pickers/tabs |
| `model.poster-slice` | 75 | enumDisplay | `Poster Slice` |  | enum case posterSlice rawValue shown in pickers/tabs |
| `model.individual-keys` | 76 | enumDisplay | `Individual Keys` |  | enum case individualKeys rawValue shown in pickers/tabs |
| `model.all-languages-universal` | 81 | enumDisplay | `All Languages (Universal)` |  | enum case all rawValue shown in pickers/tabs |
| `model.ukrainian-uk` | 82 | enumDisplay | `Ukrainian (uk)` |  | enum case uk rawValue shown in pickers/tabs |
| `model.russian-ru` | 83 | enumDisplay | `Russian (ru)` |  | enum case ru rawValue shown in pickers/tabs |
| `model.english-en` | 84 | enumDisplay | `English (en)` |  | enum case en rawValue shown in pickers/tabs |
| `model.other-fallback` | 85 | enumDisplay | `Other / Fallback` |  | enum case other rawValue shown in pickers/tabs |
| `model.spanish-es` | 86 | enumDisplay | `Spanish (es)` |  | enum case es rawValue shown in pickers/tabs |
| `model.german-de` | 87 | enumDisplay | `German (de)` |  | enum case de rawValue shown in pickers/tabs |
| `model.french-fr` | 88 | enumDisplay | `French (fr)` |  | enum case fr rawValue shown in pickers/tabs |
| `model.polish-pl` | 89 | enumDisplay | `Polish (pl)` |  | enum case pl rawValue shown in pickers/tabs |
| `model.italian-it` | 90 | enumDisplay | `Italian (it)` |  | enum case it rawValue shown in pickers/tabs |
| `model.portuguese-pt` | 91 | enumDisplay | `Portuguese (pt)` |  | enum case pt rawValue shown in pickers/tabs |
| `model.turkish-tr` | 92 | enumDisplay | `Turkish (tr)` |  | enum case tr rawValue shown in pickers/tabs |
| `model.japanese-ja` | 93 | enumDisplay | `Japanese (ja)` |  | enum case ja rawValue shown in pickers/tabs |
| `model.korean-ko` | 94 | enumDisplay | `Korean (ko)` |  | enum case ko rawValue shown in pickers/tabs |
| `model.chinese-zh` | 95 | enumDisplay | `Chinese (zh)` |  | enum case zh rawValue shown in pickers/tabs |
| `model.arabic-ar` | 96 | enumDisplay | `Arabic (ar)` |  | enum case ar rawValue shown in pickers/tabs |
| `model.hebrew-he` | 97 | enumDisplay | `Hebrew (he)` |  | enum case he rawValue shown in pickers/tabs |
| `model.universal-regular-bold` | 125 | enumDisplay | `Universal (Regular + Bold)` |  | enum case both rawValue shown in pickers/tabs |
| `model.bold-text-only-fast` | 126 | enumDisplay | `Bold Text Only (Fast)` |  | enum case boldOnly rawValue shown in pickers/tabs |
| `model.regular-font-only-fast` | 127 | enumDisplay | `Regular Font Only (Fast)` |  | enum case regularOnly rawValue shown in pickers/tabs |

### `ios-app/PairingController.swift`

| id | line | kind | English (exact) | zh-Hant | notes |
|---|---:|---|---|---|---|
| `pair.pairing-is-already-in-progress` | 47 | errorDescription | `Pairing is already in progress.` |  | LocalizedError |
| `pair.local-network-permission-is-off-enable-it-in-settings-a` | 48 | errorDescription | `Local Network permission is off. Enable it in Settings › AirCard-iOS › Local Network.` |  | LocalizedError |
| `pair.pairing-produced-an-empty-file-approve-the-pairing-requ` | 49 | errorDescription | `Pairing produced an empty file. Approve the pairing request, then try again.` |  | LocalizedError |
| `pair.cancelled` | 139 | pairingStatus | `Cancelled` |  | UI-bound pairingStatus |
| `pair.starting-local-host` | 154 | pairingStatus | `Starting local host…` |  | UI-bound pairingStatus |
| `pair.broadcasting-open-settings-to-pair` | 161 | pairingStatus | `Broadcasting… open Settings to pair` |  | UI-bound pairingStatus |
| `pair.failed-empty-pairing-file` | 236 | pairingStatus | `Failed: empty pairing file` |  | UI-bound pairingStatus |
| `pair.paired-n-nb` | 239 | pairingStatus | `Paired: \(name) (\(size)B)` |  | UI-bound pairingStatus |
| `pair.failed-n` | 243 | pairingStatus | `Failed: \(message)` |  | UI-bound pairingStatus |
| `pair.advertising-open-settings-privacy-security-developer-mo` | 262 | pairingStatus | `Advertising — open Settings › Privacy & Security › Developer Mode` |  | UI-bound pairingStatus |
| `pair.enter-pin-n-in-settings-privacy-security-developer-mode` | 267 | pairingStatus | `Enter PIN \(pin) in Settings › Privacy & Security › Developer Mode › Pair with AirCard-iOS` |  | UI-bound pairingStatus; KEEP substring `AirCard-iOS` in path (system Settings label) |

### `ios-app/TendiesEngine.swift`

| id | line | kind | English (exact) | zh-Hant | notes |
|---|---:|---|---|---|---|
| `engine.failed-to-store-wallpaper-file-at-n` | 54 | NSError | `Failed to store wallpaper file at \(destinationURL.path)` |  | may surface via errorMessage |
| `engine.failed-to-extract-tendies-zip-archive-code-n` | 76 | NSError | `Failed to extract .tendies zip archive (code \(extractRC))` |  | may surface via errorMessage |
| `engine.posterboard-container-path-is-required` | 265 | NSError | `PosterBoard Container path is required.` |  | may surface via errorMessage |
| `engine.failed-write-directory` | 473 | NSError | `Failed to write directory: \(errDesc ?? "exploit error")` |  | fixed full string with nested ?? quotes |
| `engine.failed-write-directory-default` | 473 | NSError | `exploit error` |  | nil-coalescing default inside engine.failed-write-directory |
| `engine.failed-inject-descriptor` | 563 | NSError | `Failed to inject descriptor: \(errDesc ?? "exploit error")` |  | fixed full string with nested ?? quotes |
| `engine.failed-inject-descriptor-default` | 563 | NSError | `exploit error` |  | nil-coalescing default inside engine.failed-inject-descriptor |

### `ios-app/TendiesView.swift`

| id | line | kind | English (exact) | zh-Hant | notes |
|---|---:|---|---|---|---|
| `tendies.choose-tendies-from-files` | 57 | Text | `Choose .tendies from Files…` |  |  |
| `tendies.import-more-wallpapers` | 57 | Text | `Import More Wallpapers…` |  |  |
| `tendies.posterboard-container-will-be-auto-detected-automatical` | 68 | Text | `PosterBoard container will be auto-detected automatically on flash.` |  |  |
| `tendies.target-posterboard-container-detected` | 70 | Text | `Target: PosterBoard container detected ✅` |  |  |
| `tendies.force-posterboard-cache-refresh` | 78 | Text | `Force PosterBoard Cache Refresh` |  |  |
| `tendies.resets-file-protections-so-ios-re-indexes-wallpapers-im` | 80 | Text | `Resets file protections so iOS re-indexes wallpapers immediately` |  |  |
| `tendies.n-wallpapers-imported` | 91 | Text | `\(vm.tendieItems.count) Wallpapers Imported` |  |  |
| `tendies.deselect-all` | 95 | ButtonLabel | `Deselect All` |  |  |
| `tendies.select-all` | 95 | ButtonLabel | `Select All` |  |  |
| `tendies.wallpapers-gallery` | 112 | Text | `Wallpapers Gallery` |  |  |
| `tendies.no-tendies-wallpapers-loaded-yet` | 120 | Text | `No .tendies wallpapers loaded yet` |  |  |
| `tendies.tap-choose-tendies-from-files-or-copy-wallpapers-into-o` | 123 | Text | `Tap 'Choose .tendies from Files' or copy wallpapers into On My iPhone › AirCard-iOS.` |  | KEEP substring AirCard-iOS |
| `tendies.flashing-wallpapers` | 140 | Text | `Flashing Wallpapers…` |  |  |
| `tendies.flash-n-wallpapers` | 154 | Text | `Flash \(selectedCount) Wallpaper\(selectedCount == 1 ? "" : "s")` |  | ternary Wallpaper/Wallpapers |
| `tendies.respring-neospring` | 174 | Text | `Respring (NeoSpring)` |  |  |
| `tendies.flashing-will-automatically-trigger-neospring-to-respri` | 186 | Text | `Flashing will automatically trigger NeoSpring to respring the device and apply your new wallpapers.` |  |  |
| `tendies.flash-log-n-lines` | 193 | disclosureTitle | `Flash Log (\(vm.tendiesFlashLog.count) lines)` |  |  |
| `tendies.wallpapers` | 203 | navigationTitle | `Wallpapers` |  |  |
| `tendies.n-items` | 294 | Text | `\(item.descriptorCount) item\(item.descriptorCount == 1 ? "" : "s")` |  | ternary item/items |
| `tendies.information` | 347 | Section | `Information` |  |  |
| `tendies.name` | 348 | disclosureTitle | `Name` |  |  |
| `tendies.file-name` | 349 | disclosureTitle | `File Name` |  |  |
| `tendies.type` | 350 | disclosureTitle | `Type` |  |  |
| `tendies.descriptors` | 351 | disclosureTitle | `Descriptors` |  |  |
| `tendies.target-extension` | 352 | disclosureTitle | `Target Extension` |  |  |
| `tendies.app-container` | 353 | disclosureTitle | `App Container` |  |  |
| `tendies.descriptor-archive` | 353 | disclosureTitle | `Descriptor Archive` |  |  |
| `tendies.format` | 353 | disclosureTitle | `Format` |  |  |
| `tendies.contains-sqlite-database` | 355 | disclosureTitle | `Contains SQLite database` |  |  |
| `tendies.warning` | 355 | disclosureTitle | `Warning` |  |  |
| `tendies.done` | 363 | Button | `Done` |  |  |

---

## README.md blocks

Translate headings + body prose. Keep code fences, URLs, badge image URLs, crypto addresses, and file-tree paths unchanged. Product name `AirCard-iOS` stays in headings where it is the project name.

### Block `readme.01.aircard-ios`

- **id:** `readme.01.aircard-ios`
- **file:** `README.md`
- **level:** h1
- **heading (EN):** AirCard-iOS
- **zh-Hant heading:** 
- **notes:** README section

**English body:**

```markdown
<p align="center">
  <img src="ios-app/Assets.xcassets/AppIcon.appiconset/AppIcon.png" width="128" height="128" alt="AirCard-iOS Icon" style="border-radius: 28px; box-shadow: 0 8px 24px rgba(0,0,0,0.18);" />
</p>

<p align="center">
  Apple Wallet card skins, lock screen passcode themes, and PosterBoard wallpapers directly on iOS 27+.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-iOS%2027+-blue?style=flat-square&logo=apple" alt="Platform" />
  <img src="https://img.shields.io/badge/Swift-5.0-orange?style=flat-square&logo=swift" alt="Swift" />
  <img src="https://img.shields.io/badge/Rust-FFI%20Core-red?style=flat-square&logo=rust" alt="Rust" />
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" alt="License" />
  <a href="https://www.paypal.com/donate/?hosted_button_id=98QRTC2HFRA4Y"><img src="https://img.shields.io/badge/Donate-PayPal-00457C?style=flat-square&logo=paypal" alt="Donate with PayPal" /></a>
</p>
```

**zh-Hant body:** *(blank for Trotsky)*

---

### Block `readme.02.overview`

- **id:** `readme.02.overview`
- **file:** `README.md`
- **level:** h2
- **heading (EN):** Overview
- **zh-Hant heading:** 
- **notes:** README section

**English body:**

```markdown
AirCard-iOS customizes Apple Wallet card artwork, lock screen passcode dialers, and lock screen wallpapers on device without a jailbreak.

The app communicates with internal system services over a local loopback tunnel (`10.7.0.1` or `127.0.0.1`) provided by LocalDevVPN. File operations are handled by `AirliftFFI`, a Rust library that interfaces with the AirTraffic service.

> **Compatibility**: AirCard-iOS currently requires **iOS 27.0 or newer (iOS 27+)**.
```

**zh-Hant body:** *(blank for Trotsky)*

---

### Block `readme.03.features`

- **id:** `readme.03.features`
- **file:** `README.md`
- **level:** h2
- **heading (EN):** Features
- **zh-Hant heading:** 
- **notes:** README section

**English body:**

```markdown

```

**zh-Hant body:** *(blank for Trotsky)*

---

### Block `readme.04.apple-wallet-card-skins`

- **id:** `readme.04.apple-wallet-card-skins`
- **file:** `README.md`
- **level:** h3
- **heading (EN):** Apple Wallet card skins
- **zh-Hant heading:** 
- **notes:** README section

**English body:**

```markdown
- Writes custom card artwork to Passbook caches (`cardBackgroundCombined@3x.png`, `@2x.png`, and `cardBackgroundCombined.pdf` for transit cards like Suica).
- Flushes front-face and thumbnail caches so new artwork appears immediately when Wallet opens.
- Detects card identifiers in real time when you bring up Apple Pay.
- Apply artwork to individual cards or batch-flash every detected card.
```

**zh-Hant body:** *(blank for Trotsky)*

---

### Block `readme.05.passcode-dialer-themes`

- **id:** `readme.05.passcode-dialer-themes`
- **file:** `README.md`
- **level:** h3
- **heading (EN):** Passcode dialer themes
- **zh-Hant heading:** 
- **notes:** README section

**English body:**

```markdown
- Live dialer preview with touch panning and zoom framing.
- Full poster layout across all ten buttons, or individual circular button cutouts.
- Targets system dialer caches (`TelephonyUI-10`).
- Localized number subtext options, including Ukrainian and Russian Cyrillic layouts.
- Import and export themes as `.passthm` files.
```

**zh-Hant body:** *(blank for Trotsky)*

---

### Block `readme.06.posterboard-wallpapers-tendies`

- **id:** `readme.06.posterboard-wallpapers-tendies`
- **file:** `README.md`
- **level:** h3
- **heading (EN):** PosterBoard wallpapers (.tendies)
- **zh-Hant heading:** 
- **notes:** README section

**English body:**

```markdown
- Import and unpack `.tendies` wallpaper archives directly from the Files app.
- Auto-detects PosterBoard wallpaper containers and active descriptor UUIDs.
- Injects wallpaper configurations and assets into PosterBoard storage.
- Automatically triggers a NeoSpring respring after flashing to apply wallpapers without rebooting your iPhone.
```

**zh-Hant body:** *(blank for Trotsky)*

---

### Block `readme.07.on-device-pairing`

- **id:** `readme.07.on-device-pairing`
- **file:** `README.md`
- **level:** h3
- **heading (EN):** On-device pairing
- **zh-Hant heading:** 
- **notes:** README section

**English body:**

```markdown
- Advertises locally over Bonjour so the phone can pair with itself via Settings > Privacy & Security > Developer Mode > Pair with AirCard-iOS.
- Reads and syncs pairing records automatically into `aircard_pairing.plist`.
- Once paired, no computer or external connection is needed.
```

**zh-Hant body:** *(blank for Trotsky)*

---

### Block `readme.08.prerequisites`

- **id:** `readme.08.prerequisites`
- **file:** `README.md`
- **level:** h2
- **heading (EN):** Prerequisites
- **zh-Hant heading:** 
- **notes:** README section

**English body:**

```markdown
1. **iOS 27+**: The exploit and paths currently target iOS 27.0 and above.
2. **LocalDevVPN**: Running in loopback mode (`10.7.0.1` or `127.0.0.1`) so local connections can reach internal device services.
3. **Developer Mode pairing**: Pair directly in Settings > Privacy & Security > Developer Mode > Pair with AirCard-iOS, or place an existing pairing plist in the app's documents directory.
```

**zh-Hant body:** *(blank for Trotsky)*

---

### Block `readme.09.installation`

- **id:** `readme.09.installation`
- **file:** `README.md`
- **level:** h2
- **heading (EN):** Installation
- **zh-Hant heading:** 
- **notes:** README section

**English body:**

```markdown
Install `AirCard-iOS.ipa` using your preferred sideloading method:

- SideStore or AltStore
- TrollStore
- LiveContainer
- Xcode or iOS App Signer
```

**zh-Hant body:** *(blank for Trotsky)*

---

### Block `readme.10.building-from-source`

- **id:** `readme.10.building-from-source`
- **file:** `README.md`
- **level:** h2
- **heading (EN):** Building from source
- **zh-Hant heading:** 
- **notes:** README section

**English body:**

```markdown

```

**zh-Hant body:** *(blank for Trotsky)*

---

### Block `readme.11.requirements`

- **id:** `readme.11.requirements`
- **file:** `README.md`
- **level:** h3
- **heading (EN):** Requirements
- **zh-Hant heading:** 
- **notes:** README section

**English body:**

```markdown
- macOS 14.0 or newer with Xcode 16 or newer
- XcodeGen (`brew install xcodegen`)
- Rust toolchain (only needed if rebuilding `rust-core`)
```

**zh-Hant body:** *(blank for Trotsky)*

---

### Block `readme.12.build-the-ipa`

- **id:** `readme.12.build-the-ipa`
- **file:** `README.md`
- **level:** h3
- **heading (EN):** Build the IPA
- **zh-Hant heading:** 
- **notes:** README section

**English body:**

```markdown
```bash
git clone https://github.com/mak5er/AirCard-iOS.git
cd AirCard-iOS
./build-ipa.sh
```

The completed package is written to `build/AirCard-iOS.ipa`.
```

**zh-Hant body:** *(blank for Trotsky)*

---

### Block `readme.13.rebuilding-the-rust-framework`

- **id:** `readme.13.rebuilding-the-rust-framework`
- **file:** `README.md`
- **level:** h3
- **heading (EN):** Rebuilding the Rust framework
- **zh-Hant heading:** 
- **notes:** README section

**English body:**

```markdown
To compile changes in `rust-core`:
```bash
./build-ios.sh
```
```

**zh-Hant body:** *(blank for Trotsky)*

---

### Block `readme.14.repository-structure`

- **id:** `readme.14.repository-structure`
- **file:** `README.md`
- **level:** h2
- **heading (EN):** Repository structure
- **zh-Hant heading:** 
- **notes:** README section

**English body:**

```markdown
```
AirCard-iOS/
├── ios-app/                   # SwiftUI application
│   ├── AirCardApp.swift       # App entry point and lifecycle
│   ├── AppViewModel.swift     # State management and exploit orchestration
│   ├── ContentView.swift      # Main UI views
│   ├── TendiesView.swift      # PosterBoard wallpaper view
│   ├── TendiesEngine.swift    # Tendies extraction and injection logic
│   ├── RespringHelper.swift   # NeoSpring WebKit respring implementation
│   ├── Models.swift           # Image slicing, theme layout, archive packing
│   ├── PairingController.swift# Bonjour host and pairing sync
│   ├── NetworkStatus.swift    # VPN loopback detection
│   ├── Utilities.swift        # Background keep-alive and helper functions
│   ├── GrappaHelper.[h,m]     # ATC protocol helpers
│   ├── Info.plist             # Bundle configuration
│   └── Assets.xcassets/       # App icons and image sets
├── AirliftFFI.xcframework/    # Compiled arm64 Rust static library and headers
├── rust-core/                 # Rust core source code
├── project.yml                # XcodeGen project definition
├── build-ipa.sh               # IPA build script
├── build-ios.sh               # Rust framework build script
├── LICENSE                    # MIT License
└── README.md                  # Project documentation
```
```

**zh-Hant body:** *(blank for Trotsky)*

---

### Block `readme.15.credits`

- **id:** `readme.15.credits`
- **file:** `README.md`
- **level:** h2
- **heading (EN):** Credits
- **zh-Hant heading:** 
- **notes:** README section

**English body:**

```markdown
- **[@mak5er](https://github.com/mak5er)**: Lead developer, UI, passcode theming, Tendies engine, on-device pairing.
- **[@merybist](https://github.com/merybist)**: Initial base port.
- **[AirLift](https://github.com/0xjohnnydev/airlift)** by **[0xjohnny (@0xjohnnydev)](https://github.com/0xjohnnydev)**: AirTraffic and ATAirlock sandbox escape research underlying `AirliftFFI`.
- **[NeoSpring](https://github.com/rooootdev/neospring)**: Swift implementation by **[@skadz108](https://github.com/skadz108)** and **[@rooootdev](https://github.com/rooootdev)**, and **[@neonmodder123](https://github.com/neonmodder123)** for the WebKit GPU process respring technique.
- Built upon concepts from the **AirCard** project.
```

**zh-Hant body:** *(blank for Trotsky)*

---

### Block `readme.16.support`

- **id:** `readme.16.support`
- **file:** `README.md`
- **level:** h2
- **heading (EN):** Support
- **zh-Hant heading:** 
- **notes:** README section

**English body:**

```markdown
If you want to support AirCard-iOS development:

- **PayPal**: [Donate via PayPal](https://www.paypal.com/donate/?hosted_button_id=98QRTC2HFRA4Y)
- **TON**: `UQBm9KPhtMw-XVVjirUoa09wzrlyWsbeZhKfefl1Uw-qNZ-r`
- **USDT (TRC20)**: `TDkDMCyjYxgvkWUnQiF5Erk2RyPQMT6G1n`
- **USDT / BNB (BEP20)**: `0x0954dc491c502849d04956ef74634aa5931a08e8`
```

**zh-Hant body:** *(blank for Trotsky)*

---

### Block `readme.17.license`

- **id:** `readme.17.license`
- **file:** `README.md`
- **level:** h2
- **heading (EN):** License
- **zh-Hant heading:** 
- **notes:** README section

**English body:**

```markdown
MIT License. See [LICENSE](LICENSE) for details.
```

**zh-Hant body:** *(blank for Trotsky)*

---
