# AirCard-iOS — English UI string inventory (for zh-Hant)

**Source of truth:** [Mak5er/AirCard-iOS](https://github.com/Mak5er/AirCard-iOS) `main` (shallow clone at `/workspace/AirCard-iOS-upstream`).

**Not a source of truth for wording:** [SheldonJoO/AirCard-iOS-CN](https://github.com/SheldonJoO/AirCard-iOS-CN) — used only as a *file map* of what they hardcoded.

**Translator:** Trotsky — zh-Hant filled (Taiwan Traditional Chinese). Translated from English only; CN fork not used for wording.

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
| `vm.pairing-file-loaded` | 206 | pairingStatus | `Pairing file loaded ✅ (\(originalName ?? "aircard_pairing.plist"))` | 配對檔已載入 ✅ (\(originalName ?? "aircard_pairing.plist")) | fixed full string with nested ?? quotes |
| `vm.pairing-file-loaded-default` | 206 | pairingStatus | `aircard_pairing.plist` | aircard_pairing.plist | nil-coalescing default inside vm.pairing-file-loaded; KEEP filename |
| `vm.failed-to-save-pairing-file-n` | 209 | errorMessage | `Failed to save pairing file: \(error.localizedDescription)` | 無法儲存配對檔：\(error.localizedDescription) | UI-bound errorMessage |
| `vm.starting-local-host` | 245 | pairingStatus | `Starting local host…` | 正在啟動本機主機… | UI-bound pairingStatus |
| `vm.paired-successfully` | 256 | pairingStatus | `Paired successfully! ✅` | 配對成功！✅ | UI-bound pairingStatus |
| `vm.pairing-complete-n` | 257 | activityLog | `Pairing complete: \(path)` | 配對完成：\(path) | visible in Activity/Flash Log |
| `vm.cancelled` | 261 | pairingStatus | `Cancelled.` | 已取消。 | UI-bound pairingStatus |
| `vm.pairing-failed-n` | 265 | errorMessage | `Pairing failed: \(error.localizedDescription)` | 配對失敗：\(error.localizedDescription) | UI-bound errorMessage |
| `vm.pairing-file-deleted` | 293 | pairingStatus | `Pairing file deleted` | 配對檔已刪除 | UI-bound pairingStatus |
| `vm.pairing-file-is-required-before-scanning-pair-this-ipho` | 344 | errorMessage | `Pairing file is required before scanning. Pair this iPhone or select a .plist first.` | 掃描前需要配對檔。請先配對此 iPhone，或選取一個 .plist。 | UI-bound errorMessage |
| `vm.open-apple-pay-double-click-side-button-and-tap-your-ca` | 352 | scanStatusText | `Open Apple Pay (double-click Side button) and tap your card…` | 開啟 Apple Pay（連按兩下 Side button）並輕點你的卡片… | UI-bound scanStatusText |
| `vm.started-live-card-scanner` | 354 | activityLog | `Started live card scanner…` | 已啟動即時卡片掃描… | visible in Activity/Flash Log |
| `vm.scanner-stopped-n` | 393 | scanStatusText | `Scanner stopped: \(msg)` | 掃描已停止：\(msg) | UI-bound scanStatusText |
| `vm.scanner-error-n` | 394 | activityLog | `❌ Scanner error: \(msg)` | ❌ 掃描錯誤：\(msg) | visible in Activity/Flash Log |
| `vm.card-scanner-error-n` | 395 | errorMessage | `Card scanner error: \(msg)` | 卡片掃描錯誤：\(msg) | UI-bound errorMessage |
| `vm.scanning-stopped-total-cards-n` | 397 | scanStatusText | `Scanning stopped. Total cards: \(vm.cards.count).` | 掃描已停止。卡片總數：\(vm.cards.count)。 | UI-bound scanStatusText |
| `vm.scanning-stopped-total-cards-n-2` | 398 | activityLog | `Scanning stopped. Total cards: \(vm.cards.count).` | 掃描已停止。卡片總數：\(vm.cards.count)。 | visible in Activity/Flash Log |
| `vm.scanning-stopped-total-cards-n-3` | 414 | scanStatusText | `Scanning stopped. Total cards: \(cards.count).` | 掃描已停止。卡片總數：\(cards.count)。 | UI-bound scanStatusText |
| `vm.found-card-n` | 460 | scanStatusText | `Found card: \(candidate)` | 找到卡片：\(candidate) | UI-bound scanStatusText |
| `vm.found-card-n-2` | 461 | activityLog | `Found card: \(candidate)` | 找到卡片：\(candidate) | visible in Activity/Flash Log |
| `vm.notice-loopback-vpn-not-detected-attempting-direct-loop` | 611 | activityLog | `⚠️ Notice: Loopback VPN not detected, attempting direct loopback (127.0.0.1)...` | ⚠️ 注意：未偵測到 Loopback VPN，改以直接 loopback（127.0.0.1）嘗試... | visible in Activity/Flash Log |
| `vm.n-n-flashing-card-n` | 625 | activityLog | `[\(i+1)/\(selected.count)] Flashing card \(cleanId.prefix(12))…` | [\(i+1)/\(selected.count)] 正在刷寫卡片 \(cleanId.prefix(12))… | visible in Activity/Flash Log |
| `vm.no-image-for-card-n` | 638 | activityLog | `  ⚠️ No image for card \(cleanId.prefix(8))` |   ⚠️ 卡片 \(cleanId.prefix(8)) 沒有圖片 | visible in Activity/Flash Log |
| `vm.failed-to-generate-card-skins` | 645 | activityLog | `  ⚠️ Failed to generate card skins` |   ⚠️ 無法產生卡片外觀 | visible in Activity/Flash Log |
| `vm.injecting-skins-into-n-pkpass` | 660 | activityLog | `  ⚡ Injecting skins into \(cleanId.prefix(10)).pkpass…` |   ⚡ 正在將外觀注入 \(cleanId.prefix(10)).pkpass… | visible in Activity/Flash Log |
| `vm.failed-write-card-skins` | 692 | activityLog | `  ❌ Failed to write card skins: \(errDesc ?? "exploit error")` |   ❌ 無法寫入卡片外觀：\(errDesc ?? "exploit error") | fixed full string with nested ?? quotes |
| `vm.failed-write-card-skins-default` | 692 | activityLog | `exploit error` | exploit error | nil-coalescing default inside vm.failed-write-card-skins |
| `vm.skins-applied-invalidating-pass-cache` | 698 | activityLog | `  ✅ Skins applied! Invalidating pass cache…` |   ✅ 外觀已套用！正在使通行卡快取失效… | visible in Activity/Flash Log |
| `vm.pass-cache-invalidated` | 730 | activityLog | `  ✅ Pass cache invalidated` |   ✅ 通行卡快取已失效 | visible in Activity/Flash Log |
| `vm.n-n-card-s-flashed-force-close-wallet-app-to-see-change` | 739 | activityLog | `🎉 \(successCount)/\(selected.count) card(s) flashed! Force-close Wallet app to see changes.` | 🎉 已刷寫 \(successCount)/\(selected.count) 張卡片！請強制關閉 Wallet App 以查看變更。 | visible in Activity/Flash Log |
| `vm.skins-successfully-applied-to-n-card-s-n-to-see-your-ne` | 740 | successAlertMessage | `Skins successfully applied to \(successCount) card(s)!\n\nPlease force-close the Wallet app on your iPhone (or reboot) to see your new designs.` | 已成功將外觀套用至 \(successCount) 張卡片！\n\n請在 iPhone 上強制關閉 Wallet App（或重新開機）以查看新設計。 | UI-bound successAlertMessage |
| `vm.card-flash-failed-check-connection-and-try-again` | 744 | activityLog | `❌ Card flash failed. Check connection and try again.` | ❌ 卡片刷寫失敗。請檢查連線後再試一次。 | visible in Activity/Flash Log |
| `vm.failed-to-read-passthm-invalid-or-unsupported-format` | 831 | errorMessage | `Failed to read .passthm — invalid or unsupported format.` | 無法讀取 .passthm — 格式無效或不支援。 | UI-bound errorMessage |
| `vm.no-key-images-loaded` | 880 | errorMessage | `No key images loaded.` | 尚未載入按鍵圖片。 | UI-bound errorMessage |
| `vm.notice-loopback-vpn-not-detected-attempting-direct-loop-2` | 890 | activityLog | `⚠️ Notice: Loopback VPN not detected, attempting direct loopback (127.0.0.1)...` | ⚠️ 注意：未偵測到 Loopback VPN，改以直接 loopback（127.0.0.1）嘗試... | visible in Activity/Flash Log |
| `vm.staged-theme-assets-n-langs-joined-separator` | 977 | activityLog | ⚡ Staged theme assets (\(targetVer) · \(langs.joined(separator: ", ").uppercased()) · \(targetBold.code)). Injecting into iOS caches… | ⚡ 已暫存主題資源 (\(targetVer) · \(langs.joined(separator: ", ").uppercased()) · \(targetBold.code))。正在注入到 iOS 快取… | visible in Activity/Flash Log; EN restored (source table truncated on nested backticks) |
| `vm.writing-to-n` | 1000 | activityLog | `  Writing to \(targetName)…` |   正在寫入 \(targetName)… | visible in Activity/Flash Log |
| `vm.write-to-n-failed` | 1030 | activityLog | `  ⚠️ Write to \(targetName) failed: \(lastErr ?? "error")` |   ⚠️ 寫入 \(targetName) 失敗：\(lastErr ?? "error") | fixed full string with nested ?? quotes |
| `vm.write-to-n-failed-default` | 1030 | activityLog | `error` | error | nil-coalescing default inside vm.write-to-n-failed |
| `vm.injected-into-n` | 1034 | activityLog | `  ✅ Injected into \(targetName)` |   ✅ 已注入到 \(targetName) | visible in Activity/Flash Log |
| `vm.passcode-theme-applied-lock-your-iphone-to-see-it` | 1049 | activityLog | `🎉 Passcode theme applied! Lock your iPhone to see it.` | 🎉 密碼主題已套用！請鎖定 iPhone 以查看效果。 | visible in Activity/Flash Log |
| `vm.passcode-theme-successfully-applied-n-to-see-your-new-p` | 1050 | successAlertMessage | `Passcode theme successfully applied!\n\nLock your iPhone (or restart) to see your new passcode keypad.` | 密碼主題已成功套用！\n\n請鎖定 iPhone（或重新開機）以查看新的密碼鍵盤。 | UI-bound successAlertMessage |
| `vm.one-or-more-theme-injections-failed` | 1054 | activityLog | `❌ One or more theme injections failed.` | ❌ 一或多個主題注入失敗。 | visible in Activity/Flash Log |
| `vm.please-configure-at-least-one-key-before-exporting` | 1063 | errorMessage | `Please configure at least one key before exporting.` | 匯出前請至少設定一個按鍵。 | UI-bound errorMessage |
| `vm.failed-to-export-theme-n` | 1080 | errorMessage | `Failed to export theme: \(error.localizedDescription)` | 無法匯出主題：\(error.localizedDescription) | UI-bound errorMessage |
| `vm.failed-to-import-n-n` | 1139 | errorMessage | `Failed to import \(url.lastPathComponent): \(error.localizedDescription)` | 無法匯入 \(url.lastPathComponent)：\(error.localizedDescription) | UI-bound errorMessage |
| `vm.no-pairing-file-active-pair-your-device-first-in-the-pa` | 1156 | errorMessage | `No pairing file active. Pair your device first in the Pairing tab.` | 目前沒有作用中的配對檔。請先到「配對」分頁配對裝置。 | UI-bound errorMessage |
| `vm.auto-detect-failed-n-nensure-localdevvpn-is-connected-a` | 1176 | errorMessage | `Auto-detect failed: \(error.localizedDescription)\nEnsure LocalDevVPN is connected and device is unlocked.` | 自動偵測失敗：\(error.localizedDescription)\n請確認 LocalDevVPN 已連線且裝置已解鎖。 | UI-bound errorMessage; KEEP product name LocalDevVPN |
| `vm.no-wallpapers-selected-to-flash` | 1185 | errorMessage | `No wallpapers selected to flash.` | 尚未選取要刷寫的桌布。 | UI-bound errorMessage |
| `vm.no-pairing-file-active-please-pair-your-device-first` | 1191 | errorMessage | `No pairing file active. Please pair your device first.` | 目前沒有作用中的配對檔。請先配對裝置。 | UI-bound errorMessage |
| `vm.posterboard-container-could-not-be-found-automatically-` | 1202 | errorMessage | `PosterBoard container could not be found automatically. Ensure LocalDevVPN is connected and iPhone is unlocked.` | 無法自動找到 PosterBoard 容器。請確認 LocalDevVPN 已連線且 iPhone 已解鎖。 | UI-bound errorMessage; KEEP product name LocalDevVPN |
| `vm.wallpapers-applied-successfully` | 1230 | activityLog | `🎉 Wallpapers applied successfully!` | 🎉 桌布已成功套用！ | visible in Activity/Flash Log |
| `vm.triggering-neospring-respring` | 1231 | activityLog | `⚡ Triggering NeoSpring respring...` | ⚡ 正在觸發 NeoSpring 重新載入 SpringBoard... | visible in Activity/Flash Log |
| `vm.error-n` | 1238 | activityLog | `❌ Error: \(error.localizedDescription)` | ❌ 錯誤：\(error.localizedDescription) | visible in Activity/Flash Log |
| `vm.triggering-neospring-respring-2` | 1244 | activityLog | `⚡ Triggering NeoSpring respring...` | ⚡ 正在觸發 NeoSpring 重新載入 SpringBoard... | visible in Activity/Flash Log |

### `ios-app/ContentView.swift`

| id | line | kind | English (exact) | zh-Hant | notes |
|---|---:|---|---|---|---|
| `ui.aircard-ios` | 42 | Text | `AirCard-iOS` | AirCard-iOS | KEEP TOKEN `AirCard-iOS` (Bonjour/pairing display name; CN README) |
| `ui.apple-wallet-skins-passcode-themes-for-ios-18` | 45 | Text | `Apple Wallet Skins & Passcode Themes for iOS 18+` | 適用於 iOS 18+ 的 Apple Wallet 卡片外觀與密碼主題 |  |
| `ui.lead-core-developer` | 58 | Label | `Lead & Core Developer` | 主導與核心開發者 |  |
| `ui.chief` | 62 | Text | `Chief` | 首席 |  |
| `ui.mak5er` | 72 | Text | `@mak5er` | @mak5er | KEEP proper noun / handle; KEEP proper noun/handle |
| `ui.https-github-com-mak5er` | 77 | Link | `https://github.com/mak5er` | https://github.com/mak5er |  |
| `ui.github` | 80 | Text | `GitHub` | GitHub | KEEP proper noun / handle; KEEP proper noun/handle |
| `ui.https-x-com-mak5er` | 87 | Link | `https://x.com/mak5er` | https://x.com/mak5er |  |
| `ui.twitter-x` | 90 | Text | `Twitter / X` | Twitter / X | KEEP proper noun / handle; KEEP proper noun/handle |
| `ui.base-ipa-developer` | 105 | Label | `Base IPA Developer` | 基礎 IPA 開發者 |  |
| `ui.base` | 109 | Text | `Base` | 基礎 |  |
| `ui.merybist` | 119 | Text | `@merybist` | @merybist | KEEP proper noun / handle; KEEP proper noun/handle |
| `ui.https-github-com-merybist` | 124 | Link | `https://github.com/merybist` | https://github.com/merybist |  |
| `ui.github-2` | 127 | Text | `GitHub` | GitHub | KEEP proper noun / handle; KEEP proper noun/handle |
| `ui.https-x-com-merybist` | 134 | Link | `https://x.com/merybist` | https://x.com/merybist |  |
| `ui.twitter-x-2` | 137 | Text | `Twitter / X` | Twitter / X | KEEP proper noun / handle; KEEP proper noun/handle |
| `ui.core-exploit` | 156 | Text | `Core Exploit` | 核心 Exploit |  |
| `ui.airlift-airtraffic-sync-sandbox-escape` | 158 | Text | `airlift (AirTraffic sync sandbox escape)` | airlift（AirTraffic 同步沙盒逃逸） |  |
| `ui.passcode-themes` | 171 | Text | `Passcode Themes` | 密碼主題 |  |
| `ui.neospring-posterboard` | 186 | Text | `NeoSpring & PosterBoard` | NeoSpring & PosterBoard |  |
| `ui.springboard-reload-tendies-wallpapers-neonmodder123-ska` | 188 | Text | `SpringBoard reload & .tendies wallpapers (@neonmodder123, @skadz108, @rooootdev)` | SpringBoard 重新載入與 .tendies 桌布（@neonmodder123、@skadz108、@rooootdev） |  |
| `ui.credits` | 204 | navigationTitle | `Credits` | 致謝 |  |
| `ui.done` | 208 | Button | `Done` | 完成 |  |
| `ui.copied` | 262 | Text | `Copied` | 已複製 | CompactLogView after copy |
| `ui.pairing` | 358 | Label | `Pairing` | 配對 |  |
| `ui.wallet-cards` | 362 | Label | `Wallet Cards` | Wallet 卡片 |  |
| `ui.passcode` | 366 | Label | `Passcode` | 密碼 |  |
| `ui.wallpapers` | 370 | Label | `Wallpapers` | 桌布 |  |
| `ui.notice` | 373 | alert | `Notice` | 注意 |  |
| `ui.ok` | 377 | Button | `OK` | 確定 |  |
| `ui.success` | 381 | alert | `Success! 🎉` | 成功！🎉 |  |
| `ui.ok-2` | 382 | Button | `OK` | 確定 |  |
| `ui.aircard-ios-2` | 415 | Text | `AirCard-iOS` | AirCard-iOS | KEEP TOKEN `AirCard-iOS` (Bonjour/pairing display name; CN README) |
| `ui.ios-n-v1-3` | 418 | Text | `iOS \(ProcessInfo.processInfo.operatingSystemVersion.majorVersion) · v1.3` | iOS \(ProcessInfo.processInfo.operatingSystemVersion.majorVersion) · v1.3 |  |
| `ui.apply-custom-wallet-card-skins-and-passcode-themes-on-d` | 425 | Text | `Apply custom wallet card skins and passcode themes on-device using the AirTraffic sandbox escape.` | 透過 AirTraffic 沙盒逃逸，在裝置上套用自訂 Wallet 卡片外觀與密碼主題。 |  |
| `ui.network` | 433 | Section | `Network` | 網路 |  |
| `ui.active-pairing` | 438 | Section | `Active Pairing` | 作用中的配對 |  |
| `ui.ready-to-exploit` | 443 | Text | `Ready to exploit ✅` | 已準備好執行 exploit ✅ |  |
| `ui.n-n` | 445 | Text | `\(vm.pairingFileName) (\(vm.pairingFileSizeString))` | \(vm.pairingFileName) (\(vm.pairingFileSizeString)) |  |
| `ui.not-paired` | 452 | Text | `Not Paired` | 尚未配對 |  |
| `ui.tap-pair-this-iphone-below-to-pair` | 454 | Text | `Tap 'Pair This iPhone' below to pair.` | 輕點下方「配對此 iPhone」以進行配對。 |  |
| `ui.delete-pairing-session` | 472 | confirmationDialog | `Delete pairing session?` | 要刪除配對工作階段嗎？ |  |
| `ui.delete` | 476 | Button | `Delete` | 刪除 |  |
| `ui.cancel` | 477 | Button | `Cancel` | 取消 |  |
| `ui.delete-pairing-message` | 479 | Text | `The active pairing credentials will be removed.` | 作用中的配對憑證將會被移除。 | confirmationDialog message |
| `ui.pair-on-this-iphone` | 483 | Section | `Pair on This iPhone` | 在此 iPhone 上配對 |  |
| `ui.starting-local-pairing-host` | 488 | Text | `Starting local pairing host…` | 正在啟動本機配對主機… |  |
| `ui.enter-this-pin-on-this-iphone` | 495 | Text | `ENTER THIS PIN ON THIS IPHONE:` | 請在此 iPhone 輸入此 PIN： |  |
| `ui.copy-2` | 508 | Label | `Copy` | 複製 |  |
| `ui.settings-privacy-security-developer-mode-pair-with-airc` | 515 | Text | `Settings › Privacy & Security › Developer Mode › Pair with AirCard-iOS` | 設定 › 隱私權與安全性 › 開發人員模式 › Pair with AirCard-iOS | KEEP substring `AirCard-iOS` in path (system Settings label) |
| `ui.open-settings-app-now` | 524 | Label | `Open Settings App Now` | 立即開啟「設定」App |  |
| `ui.cancel-pairing` | 542 | Text | `Cancel Pairing` | 取消配對 |  |
| `ui.pair-this-iphone` | 573 | Text | `Pair This iPhone` | 配對此 iPhone |  |
| `ui.re-pair-this-iphone` | 573 | Text | `Re-Pair This iPhone` | 重新配對此 iPhone |  |
| `ui.activity-log-n-lines` | 589 | disclosureTitle | `Activity Log (\(vm.log.count) lines)` | 活動紀錄（\(vm.log.count) 行） |  |
| `ui.aircard-ios-3` | 599 | navigationTitle | `AirCard-iOS` | AirCard-iOS | KEEP TOKEN `AirCard-iOS` (Bonjour/pairing display name; CN README) |
| `ui.credits-2` | 609 | Text | `Credits` | 致謝 |  |
| `ui.loopback-vpn-active` | 649 | Text | `Loopback VPN Active` | Loopback VPN 作用中 |  |
| `ui.loopback-vpn-not-detected` | 649 | Text | `Loopback VPN Not Detected` | 未偵測到 Loopback VPN |  |
| `ui.rsd-tunnel-ready` | 652 | Text | `RSD tunnel ready — exploit will connect.` | RSD 通道就緒 — exploit 即將連線。 |  |
| `ui.connect-localdevvpn-before-flashes` | 653 | Text | `Connect LocalDevVPN before running flashes.` | 執行刷寫前請先連線 LocalDevVPN。 | KEEP product name LocalDevVPN |
| `ui.setup-localdevvpn` | 661 | Text | `Setup LocalDevVPN:` | 設定 LocalDevVPN： | KEEP product name LocalDevVPN |
| `ui.1-open-localdevvpn-app-and-tap-connect` | 664 | instructionStep | `1. Open LocalDevVPN app and tap Connect.` | 1. 開啟 LocalDevVPN App 並輕點連線。 | VPN/setup instruction step; KEEP product name LocalDevVPN |
| `ui.2-return-to-aircard-ios-status-indicator-turns-green` | 665 | instructionStep | `2. Return to AirCard-iOS — status indicator turns green.` | 2. 返回 AirCard-iOS — 狀態指示會變成綠色。 | VPN/setup instruction step |
| `ui.launch-localdevvpn` | 671 | Link | `Launch LocalDevVPN` | 啟動 LocalDevVPN | KEEP product name LocalDevVPN |
| `ui.device-ip` | 681 | Text | `Device IP:` | 裝置 IP： |  |
| `ui.assign-card-skin` | 804 | Text | `Assign Card Skin` | 指定卡片外觀 |  |
| `ui.tap-to-choose-photo` | 808 | Text | `Tap to choose photo` | 輕點以選擇照片 |  |
| `ui.card-n` | 830 | Text | `Card #\(cardIndex + 1)` | 卡片 #\(cardIndex + 1) |  |
| `ui.wallet-cards-n` | 931 | navigationTitle | `Wallet Cards (\(vm.cards.count))` | Wallet 卡片（\(vm.cards.count)） |  |
| `ui.scan-cards` | 939 | Text | `Scan Cards` | 掃描卡片 |  |
| `ui.stop-scan` | 939 | Text | `Stop Scan` | 停止掃描 |  |
| `ui.add-card-manually` | 951 | Label | `Add Card Manually` | 手動新增卡片 |  |
| `ui.set-skin-for-all-cards` | 958 | Label | `Set Skin for All Cards...` | 為所有卡片設定外觀... |  |
| `ui.select-all` | 966 | Label | `Select All` | 全選 |  |
| `ui.deselect-all` | 972 | Label | `Deselect All` | 取消全選 |  |
| `ui.clear-all-cards` | 982 | Label | `Clear All Cards` | 清除所有卡片 |  |
| `ui.credits-3` | 990 | Label | `Credits` | 致謝 |  |
| `ui.choose-image-source` | 1013 | confirmationDialog | `Choose Image Source` | 選擇圖片來源 |  |
| `ui.photo-library` | 1017 | Label | `Photo Library` | 照片圖庫 |  |
| `ui.choose-from-files` | 1022 | Label | `Choose from Files…` | 從「檔案」選擇… |  |
| `ui.cancel-2` | 1024 | Button | `Cancel` | 取消 |  |
| `ui.live-scanner-active` | 1086 | Text | `Live Scanner Active` | 即時掃描作用中 |  |
| `ui.scanner-status` | 1092 | Text | `Scanner Status` | 掃描狀態 |  |
| `ui.stop` | 1098 | Button | `Stop` | 停止 |  |
| `ui.flash-log-n-lines` | 1149 | disclosureTitle | `Flash Log (\(vm.cardFlashLog.count) lines)` | 刷寫紀錄（\(vm.cardFlashLog.count) 行） |  |
| `ui.flashing` | 1169 | Text | `Flashing…` | 刷寫中… |  |
| `ui.retry` | 1174 | Text | `Retry` | 重試 |  |
| `ui.flash` | 1179 | Text | `Flash` | 刷寫 |  |
| `ui.no-cards-detected-yet` | 1203 | Text | `No Cards Detected Yet` | 尚未偵測到卡片 |  |
| `ui.tap-scan-cards-in-the-toolbar-above` | 1211 | Text | `Tap **Scan Cards** in the toolbar above.` | 輕點上方工具列的 **掃描卡片**。 |  |
| `ui.on-this-iphone-double-click-the-side-button-apple-pay-a` | 1217 | Text | `On this iPhone, **double-click the Side button** (Apple Pay), authenticate with **Face ID**, and **tap your card**.` | 在此 iPhone 上，**連按兩下 Side button**（Apple Pay），以 **Face ID** 驗證，然後**輕點你的卡片**。 |  |
| `ui.your-card-will-appear-here-automatically` | 1223 | Text | `Your card will appear here automatically!` | 你的卡片會自動出現在這裡！ |  |
| `ui.scan-cards-2` | 1240 | Text | `Scan Cards` | 掃描卡片 |  |
| `ui.stop-scan-2` | 1240 | Text | `Stop Scan` | 停止掃描 |  |
| `ui.add-manually` | 1257 | Text | `Add Manually` | 手動新增 |  |
| `ui.card-hash` | 1285 | Section | `Card Hash` | 卡片雜湊 |  |
| `ui.paste-card-hash-e-g-m6ndwzrkybfl` | 1286 | TextField | `Paste card hash (e.g. M6nDwZrkYbFl…)` | 貼上卡片雜湊（例如 M6nDwZrkYbFl…） |  |
| `ui.you-can-add-multiple-hashes-at-once-separate-them-with-` | 1293 | Text | `You can add multiple hashes at once — separate them with spaces, commas, or newlines.` | 可一次新增多個雜湊 — 以空格、逗號或換行分隔。 |  |
| `ui.add-card` | 1298 | navigationTitle | `Add Card` | 新增卡片 |  |
| `ui.cancel-3` | 1302 | Button | `Cancel` | 取消 |  |
| `ui.add` | 1305 | Button | `Add` | 新增 |  |
| `ui.mode` | 1325 | Picker | `Mode` | 模式 | Picker label (segmented Apply/Create) |
| `ui.flash-log-n-lines-2` | 1343 | disclosureTitle | `Flash Log (\(vm.passthmFlashLog.count) lines)` | 刷寫紀錄（\(vm.passthmFlashLog.count) 行） |  |
| `ui.passcode-theme` | 1353 | navigationTitle | `Passcode Theme` | 密碼主題 |  |
| `ui.themes-in-app-folder-on-my-iphone-aircard-ios` | 1381 | Section | `Themes in App Folder (On My iPhone › AirCard-iOS)` | App 資料夾中的主題（我的 iPhone › AirCard-iOS） | KEEP substring AirCard-iOS |
| `ui.load` | 1389 | Button | `Load` | 載入 |  |
| `ui.browse-files` | 1400 | Section | `Browse Files` | 瀏覽檔案 |  |
| `ui.change-passthm` | 1405 | Label | `Change .passthm…` | 更換 .passthm… |  |
| `ui.choose-passthm-from-files` | 1405 | Label | `Choose .passthm from Files…` | 從「檔案」選擇 .passthm… |  |
| `ui.clear` | 1414 | Text | `Clear` | 清除 |  |
| `ui.interactive-lock-screen-preview` | 1433 | Section | `Interactive Lock Screen Preview` | 互動式鎖定畫面預覽 |  |
| `ui.theme-information` | 1439 | Section | `Theme Information` | 主題資訊 |  |
| `ui.files-in-theme` | 1440 | LabeledContent | `Files in theme` | 主題中的檔案 |  |
| `ui.digits-styled` | 1441 | LabeledContent | `Digits styled` | 已設定數字樣式 |  |
| `ui.n-keys` | 1441 | LabeledContentValue | `\(theme.keysPreview.count) keys` | \(theme.keysPreview.count) 個按鍵 | value template next to Digits styled |
| `ui.edit-in-theme-creator` | 1446 | Label | `Edit in Theme Creator` | 在主題建立器中編輯 |  |
| `ui.remove-unload-theme` | 1464 | Text | `Remove / Unload Theme` | 移除／卸載主題 |  |
| `ui.flashing-theme` | 1485 | Text | `Flashing Theme…` | 正在刷寫主題… |  |
| `ui.retry-flash-theme` | 1497 | Text | `Retry Flash Theme` | 重試刷寫主題 |  |
| `ui.flash-theme-to-iphone` | 1514 | Text | `Flash Theme to iPhone` | 將主題刷寫到 iPhone |  |
| `ui.flash-language-target` | 1539 | Text | `Flash & Language Target` | 刷寫與語言目標 |  |
| `ui.system-caches` | 1545 | Text | `System Caches` | 系統快取 |  |
| `ui.telephonyui-10-ios-18` | 1549 | Text | `TelephonyUI-10 (iOS 18+)` | TelephonyUI-10（iOS 18+） | KEEP cache folder name TelephonyUI-N; translate parenthetical only if desired |
| `ui.telephonyui-9-ios-16-17` | 1550 | Text | `TelephonyUI-9 (iOS 16–17)` | TelephonyUI-9（iOS 16–17） | KEEP cache folder name TelephonyUI-N; translate parenthetical only if desired |
| `ui.telephonyui-8-ios-14-15` | 1551 | Text | `TelephonyUI-8 (iOS 14–15)` | TelephonyUI-8（iOS 14–15） | KEEP cache folder name TelephonyUI-N; translate parenthetical only if desired |
| `ui.universal-all` | 1552 | Text | `Universal (All)` | 通用（全部） |  |
| `ui.system-language` | 1562 | Text | `System Language` | 系統語言 |  |
| `ui.font-weight-style` | 1578 | Text | `Font Weight / Style` | 字重／樣式 |  |
| `ui.universal-mode-flashes-600-files-for-all-languages-bold` | 1598 | Text | `Universal mode flashes ~600 files for all languages & Bold text. Selecting a specific language (e.g. Ukrainian) speeds up flashing dramatically.` | 通用模式會刷寫約 600 個檔案，涵蓋所有語言與粗體文字。選取特定語言（例如烏克蘭文）可大幅加快刷寫速度。 |  |
| `ui.fast-mode-selected-only-targets-n-with-n` | 1603 | Text | `Fast mode selected: only targets \(vm.passcodeLanguageTarget.rawValue) with \(vm.passcodeBoldTarget.rawValue).` | 已選取快速模式：僅針對 \(vm.passcodeLanguageTarget.rawValue) 與 \(vm.passcodeBoldTarget.rawValue)。 |  |
| `ui.slice-mode` | 1631 | Section | `Slice Mode` | 裁切模式 |  |
| `ui.interactive-lock-screen-preview-2` | 1647 | Section | `Interactive Lock Screen Preview` | 互動式鎖定畫面預覽 |  |
| `ui.export-passthm` | 1667 | Text | `Export .passthm...` | 匯出 .passthm... |  |
| `ui.clear-all` | 1682 | Text | `Clear All` | 全部清除 |  |
| `ui.poster-image` | 1699 | Section | `Poster Image` | 海報圖片 |  |
| `ui.change-photo` | 1703 | Label | `Change Photo…` | 更換照片… |  |
| `ui.select-photo-for-keypad` | 1703 | Label | `Select Photo for Keypad…` | 為鍵盤選擇照片… |  |
| `ui.choose-poster-image-source` | 1708 | confirmationDialog | `Choose Poster Image Source` | 選擇海報圖片來源 |  |
| `ui.photo-library-2` | 1712 | Label | `Photo Library` | 照片圖庫 |  |
| `ui.choose-from-files-2` | 1717 | Label | `Choose from Files…` | 從「檔案」選擇… |  |
| `ui.cancel-4` | 1719 | Button | `Cancel` | 取消 |  |
| `ui.slicing-style` | 1750 | Section | `Slicing Style` | 裁切樣式 |  |
| `ui.seamless-poster` | 1753 | Text | `Seamless Poster` | 無縫海報 |  |
| `ui.circle-buttons` | 1754 | Text | `Circle Buttons` | 圓形按鈕 |  |
| `ui.artwork-is-clipped-into-individual-circular-button-icon` | 1761 | Text | `Artwork is clipped into individual circular button icons.` | 圖稿會裁切成個別的圓形按鈕圖示。 |  |
| `ui.seamless-artwork-spans-across-dialer-keys-without-circu` | 1761 | Text | `Seamless artwork spans across dialer keys without circular cuts (Adobe Dog style).` | 無縫圖稿會橫跨撥號鍵，不做圓形裁切（Adobe Dog 風格）。 |  |
| `ui.zoom-framing` | 1772 | Text | `Zoom & Framing` | 縮放與構圖 |  |
| `ui.reset-position` | 1776 | Button | `Reset Position` | 重設位置 |  |
| `ui.1fx` | 1799 | Text | `%.1fx` | %.1fx |  |
| `ui.drag-anywhere-on-the-dialer-preview-to-reposition` | 1808 | Text | `Drag anywhere on the dialer preview to reposition` | 在撥號鍵盤預覽上任意拖曳以重新定位 |  |
| `ui.individual-keys` | 1820 | Section | `Individual Keys` | 個別按鍵 |  |
| `ui.tap-a-button-row-to-assign-a-custom-image` | 1821 | Text | `Tap a button row to assign a custom image.` | 輕點按鍵列以指定自訂圖片。 |  |
| `ui.key-n` | 1844 | Text | `Key \(btn.digit)` | 按鍵 \(btn.digit) |  |
| `ui.choose-key-n-image-source-default` | 1877 | confirmationDialog | `` | `` | nil-coalescing default inside ui.choose-key-n-image-source; KEEP empty string |
| `ui.choose-key-n-image-source` | 1877 | confirmationDialog | `Choose Key \(selectedDigitForPicker ?? "") Image Source` | 選擇按鍵 \(selectedDigitForPicker ?? "") 的圖片來源 | fixed full string with nested ?? quotes |
| `ui.photo-library-3` | 1881 | Label | `Photo Library` | 照片圖庫 |  |
| `ui.choose-from-files-3` | 1886 | Label | `Choose from Files…` | 從「檔案」選擇… |  |
| `ui.cancel-5` | 1888 | Button | `Cancel` | 取消 |  |
| `ui.flashing-theme-2` | 1937 | Text | `Flashing Theme…` | 正在刷寫主題… |  |
| `ui.retry-flash-theme-2` | 1949 | Text | `Retry Flash Theme` | 重試刷寫主題 |  |
| `ui.flash-theme-to-iphone-2` | 1966 | Text | `Flash Theme to iPhone` | 將主題刷寫到 iPhone |  |
| `ui.drag-preview-to-reposition` | 2080 | Text | `Drag preview to reposition` | 拖曳預覽以重新定位 |  |

### `ios-app/Info.plist`

| id | line | kind | English (exact) | zh-Hant | notes |
|---|---:|---|---|---|---|
| `plist.aircard-ios` | 8 | Info.plist | `AirCard-iOS` | AirCard-iOS | KEEP ENGLISH — display/pairing service name (CN README); KEEP TOKEN `AirCard-iOS` (Bonjour/pairing display name; CN README) |
| `plist.aircard-ios-advertises-an-on-device-pairing-service-so-` | 38 | Info.plist | `AirCard-iOS advertises an on-device pairing service so this iPhone can pair with itself, and connects to the local lockdown daemon to run the exploit.` | AirCard-iOS 會在裝置上提供配對服務，讓此 iPhone 能與自身配對，並連線到本機 lockdown 守護程式以執行 exploit。 | Info.plist user-visible; KEEP TOKEN `AirCard-iOS` (Bonjour/pairing display name; CN README) |
| `plist.aircard-ios-needs-photo-access-to-apply-custom-card-ski` | 40 | Info.plist | `AirCard-iOS needs photo access to apply custom card skins and passcode themes.` | AirCard-iOS 需要取用照片，才能套用自訂卡片外觀與密碼主題。 | Info.plist user-visible; KEEP TOKEN `AirCard-iOS` (Bonjour/pairing display name; CN README) |
| `plist.passcode-theme` | 62 | Info.plist | `Passcode Theme` | 密碼主題 | Info.plist user-visible |
| `plist.pairing-file` | 74 | Info.plist | `Pairing File` | 配對檔 | Info.plist user-visible |
| `plist.posterboard-wallpaper` | 86 | Info.plist | `PosterBoard Wallpaper` | PosterBoard 桌布 | Info.plist user-visible |
| `plist.passcode-theme-archive` | 103 | Info.plist | `Passcode Theme Archive` | 密碼主題封存檔 | Info.plist user-visible |
| `plist.posterboard-wallpaper-archive` | 121 | Info.plist | `PosterBoard Wallpaper Archive` | PosterBoard 桌布封存檔 | Info.plist user-visible |
| `plist.posterboard-wallpaper-archive-2` | 143 | Info.plist | `PosterBoard Wallpaper Archive` | PosterBoard 桌布封存檔 | Info.plist user-visible |
| `plist.passcode-theme-archive-2` | 162 | Info.plist | `Passcode Theme Archive` | 密碼主題封存檔 | Info.plist user-visible |

### `ios-app/Models.swift`

| id | line | kind | English (exact) | zh-Hant | notes |
|---|---:|---|---|---|---|
| `model.pairing` | 52 | enumDisplay | `Pairing` | 配對 | enum case pairing rawValue shown in pickers/tabs |
| `model.wallet-cards` | 53 | enumDisplay | `Wallet Cards` | Wallet 卡片 | enum case walletCards rawValue shown in pickers/tabs |
| `model.passcode` | 54 | enumDisplay | `Passcode` | 密碼 | enum case passcodeThemes rawValue shown in pickers/tabs |
| `model.wallpapers` | 55 | enumDisplay | `Wallpapers` | 桌布 | enum case wallpapers rawValue shown in pickers/tabs |
| `model.apply-passthm` | 69 | enumDisplay | `Apply .passthm` | 套用 .passthm | enum case applyTheme rawValue shown in pickers/tabs |
| `model.create-theme` | 70 | enumDisplay | `Create Theme` | 建立主題 | enum case themeCreator rawValue shown in pickers/tabs |
| `model.poster-slice` | 75 | enumDisplay | `Poster Slice` | 海報裁切 | enum case posterSlice rawValue shown in pickers/tabs |
| `model.individual-keys` | 76 | enumDisplay | `Individual Keys` | 個別按鍵 | enum case individualKeys rawValue shown in pickers/tabs |
| `model.all-languages-universal` | 81 | enumDisplay | `All Languages (Universal)` | 所有語言（通用） | enum case all rawValue shown in pickers/tabs |
| `model.ukrainian-uk` | 82 | enumDisplay | `Ukrainian (uk)` | 烏克蘭文 (uk) | enum case uk rawValue shown in pickers/tabs |
| `model.russian-ru` | 83 | enumDisplay | `Russian (ru)` | 俄文 (ru) | enum case ru rawValue shown in pickers/tabs |
| `model.english-en` | 84 | enumDisplay | `English (en)` | 英文 (en) | enum case en rawValue shown in pickers/tabs |
| `model.other-fallback` | 85 | enumDisplay | `Other / Fallback` | 其他／備用 | enum case other rawValue shown in pickers/tabs |
| `model.spanish-es` | 86 | enumDisplay | `Spanish (es)` | 西班牙文 (es) | enum case es rawValue shown in pickers/tabs |
| `model.german-de` | 87 | enumDisplay | `German (de)` | 德文 (de) | enum case de rawValue shown in pickers/tabs |
| `model.french-fr` | 88 | enumDisplay | `French (fr)` | 法文 (fr) | enum case fr rawValue shown in pickers/tabs |
| `model.polish-pl` | 89 | enumDisplay | `Polish (pl)` | 波蘭文 (pl) | enum case pl rawValue shown in pickers/tabs |
| `model.italian-it` | 90 | enumDisplay | `Italian (it)` | 義大利文 (it) | enum case it rawValue shown in pickers/tabs |
| `model.portuguese-pt` | 91 | enumDisplay | `Portuguese (pt)` | 葡萄牙文 (pt) | enum case pt rawValue shown in pickers/tabs |
| `model.turkish-tr` | 92 | enumDisplay | `Turkish (tr)` | 土耳其文 (tr) | enum case tr rawValue shown in pickers/tabs |
| `model.japanese-ja` | 93 | enumDisplay | `Japanese (ja)` | 日文 (ja) | enum case ja rawValue shown in pickers/tabs |
| `model.korean-ko` | 94 | enumDisplay | `Korean (ko)` | 韓文 (ko) | enum case ko rawValue shown in pickers/tabs |
| `model.chinese-zh` | 95 | enumDisplay | `Chinese (zh)` | 中文 (zh) | enum case zh rawValue shown in pickers/tabs |
| `model.arabic-ar` | 96 | enumDisplay | `Arabic (ar)` | 阿拉伯文 (ar) | enum case ar rawValue shown in pickers/tabs |
| `model.hebrew-he` | 97 | enumDisplay | `Hebrew (he)` | 希伯來文 (he) | enum case he rawValue shown in pickers/tabs |
| `model.universal-regular-bold` | 125 | enumDisplay | `Universal (Regular + Bold)` | 通用（一般 + 粗體） | enum case both rawValue shown in pickers/tabs |
| `model.bold-text-only-fast` | 126 | enumDisplay | `Bold Text Only (Fast)` | 僅粗體文字（快速） | enum case boldOnly rawValue shown in pickers/tabs |
| `model.regular-font-only-fast` | 127 | enumDisplay | `Regular Font Only (Fast)` | 僅一般字體（快速） | enum case regularOnly rawValue shown in pickers/tabs |

### `ios-app/PairingController.swift`

| id | line | kind | English (exact) | zh-Hant | notes |
|---|---:|---|---|---|---|
| `pair.pairing-is-already-in-progress` | 47 | errorDescription | `Pairing is already in progress.` | 配對已在進行中。 | LocalizedError |
| `pair.local-network-permission-is-off-enable-it-in-settings-a` | 48 | errorDescription | `Local Network permission is off. Enable it in Settings › AirCard-iOS › Local Network.` | 「區域網路」權限已關閉。請到設定 › AirCard-iOS › 區域網路 開啟。 | LocalizedError |
| `pair.pairing-produced-an-empty-file-approve-the-pairing-requ` | 49 | errorDescription | `Pairing produced an empty file. Approve the pairing request, then try again.` | 配對產生了空白檔案。請核准配對要求後再試一次。 | LocalizedError |
| `pair.cancelled` | 139 | pairingStatus | `Cancelled` | 已取消 | UI-bound pairingStatus |
| `pair.starting-local-host` | 154 | pairingStatus | `Starting local host…` | 正在啟動本機主機… | UI-bound pairingStatus |
| `pair.broadcasting-open-settings-to-pair` | 161 | pairingStatus | `Broadcasting… open Settings to pair` | 廣播中…請開啟「設定」以配對 | UI-bound pairingStatus |
| `pair.failed-empty-pairing-file` | 236 | pairingStatus | `Failed: empty pairing file` | 失敗：空白配對檔 | UI-bound pairingStatus |
| `pair.paired-n-nb` | 239 | pairingStatus | `Paired: \(name) (\(size)B)` | 已配對：\(name)（\(size)B） | UI-bound pairingStatus |
| `pair.failed-n` | 243 | pairingStatus | `Failed: \(message)` | 失敗：\(message) | UI-bound pairingStatus |
| `pair.advertising-open-settings-privacy-security-developer-mo` | 262 | pairingStatus | `Advertising — open Settings › Privacy & Security › Developer Mode` | 廣播中 — 請開啟設定 › 隱私權與安全性 › 開發人員模式 | UI-bound pairingStatus |
| `pair.enter-pin-n-in-settings-privacy-security-developer-mode` | 267 | pairingStatus | `Enter PIN \(pin) in Settings › Privacy & Security › Developer Mode › Pair with AirCard-iOS` | 在設定 › 隱私權與安全性 › 開發人員模式 › Pair with AirCard-iOS 輸入 PIN \(pin) | UI-bound pairingStatus; KEEP substring `AirCard-iOS` in path (system Settings label) |

### `ios-app/TendiesEngine.swift`

| id | line | kind | English (exact) | zh-Hant | notes |
|---|---:|---|---|---|---|
| `engine.failed-to-store-wallpaper-file-at-n` | 54 | NSError | `Failed to store wallpaper file at \(destinationURL.path)` | 無法將桌布檔案儲存到 \(destinationURL.path) | may surface via errorMessage |
| `engine.failed-to-extract-tendies-zip-archive-code-n` | 76 | NSError | `Failed to extract .tendies zip archive (code \(extractRC))` | 無法解壓縮 .tendies zip 封存檔（代碼 \(extractRC)） | may surface via errorMessage |
| `engine.posterboard-container-path-is-required` | 265 | NSError | `PosterBoard Container path is required.` | 需要 PosterBoard 容器路徑。 | may surface via errorMessage |
| `engine.failed-write-directory` | 473 | NSError | `Failed to write directory: \(errDesc ?? "exploit error")` | 無法寫入目錄：\(errDesc ?? "exploit error") | fixed full string with nested ?? quotes |
| `engine.failed-write-directory-default` | 473 | NSError | `exploit error` | exploit error | nil-coalescing default inside engine.failed-write-directory |
| `engine.failed-inject-descriptor` | 563 | NSError | `Failed to inject descriptor: \(errDesc ?? "exploit error")` | 無法注入 descriptor：\(errDesc ?? "exploit error") | fixed full string with nested ?? quotes |
| `engine.failed-inject-descriptor-default` | 563 | NSError | `exploit error` | exploit error | nil-coalescing default inside engine.failed-inject-descriptor |

### `ios-app/TendiesView.swift`

| id | line | kind | English (exact) | zh-Hant | notes |
|---|---:|---|---|---|---|
| `tendies.choose-tendies-from-files` | 57 | Text | `Choose .tendies from Files…` | 從「檔案」選擇 .tendies… |  |
| `tendies.import-more-wallpapers` | 57 | Text | `Import More Wallpapers…` | 匯入更多桌布… |  |
| `tendies.posterboard-container-will-be-auto-detected-automatical` | 68 | Text | `PosterBoard container will be auto-detected automatically on flash.` | 刷寫時會自動偵測 PosterBoard 容器。 |  |
| `tendies.target-posterboard-container-detected` | 70 | Text | `Target: PosterBoard container detected ✅` | 目標：已偵測到 PosterBoard 容器 ✅ |  |
| `tendies.force-posterboard-cache-refresh` | 78 | Text | `Force PosterBoard Cache Refresh` | 強制重新整理 PosterBoard 快取 |  |
| `tendies.resets-file-protections-so-ios-re-indexes-wallpapers-im` | 80 | Text | `Resets file protections so iOS re-indexes wallpapers immediately` | 重設檔案保護，讓 iOS 立即重新索引桌布 |  |
| `tendies.n-wallpapers-imported` | 91 | Text | `\(vm.tendieItems.count) Wallpapers Imported` | 已匯入 \(vm.tendieItems.count) 張桌布 |  |
| `tendies.deselect-all` | 95 | ButtonLabel | `Deselect All` | 取消全選 |  |
| `tendies.select-all` | 95 | ButtonLabel | `Select All` | 全選 |  |
| `tendies.wallpapers-gallery` | 112 | Text | `Wallpapers Gallery` | 桌布圖庫 |  |
| `tendies.no-tendies-wallpapers-loaded-yet` | 120 | Text | `No .tendies wallpapers loaded yet` | 尚未載入 .tendies 桌布 |  |
| `tendies.tap-choose-tendies-from-files-or-copy-wallpapers-into-o` | 123 | Text | `Tap 'Choose .tendies from Files' or copy wallpapers into On My iPhone › AirCard-iOS.` | 輕點「從『檔案』選擇 .tendies」，或將桌布複製到「我的 iPhone › AirCard-iOS」。 | KEEP substring AirCard-iOS |
| `tendies.flashing-wallpapers` | 140 | Text | `Flashing Wallpapers…` | 正在刷寫桌布… |  |
| `tendies.flash-n-wallpapers` | 154 | Text | `Flash \(selectedCount) Wallpaper\(selectedCount == 1 ? "" : "s")` | 刷寫 \(selectedCount) 張桌布\(selectedCount == 1 ? "" : "s") | ternary Wallpaper/Wallpapers |
| `tendies.respring-neospring` | 174 | Text | `Respring (NeoSpring)` | 重新載入 SpringBoard（NeoSpring） |  |
| `tendies.flashing-will-automatically-trigger-neospring-to-respri` | 186 | Text | `Flashing will automatically trigger NeoSpring to respring the device and apply your new wallpapers.` | 刷寫完成後會自動觸發 NeoSpring，重新載入裝置並套用新桌布。 |  |
| `tendies.flash-log-n-lines` | 193 | disclosureTitle | `Flash Log (\(vm.tendiesFlashLog.count) lines)` | 刷寫紀錄（\(vm.tendiesFlashLog.count) 行） |  |
| `tendies.wallpapers` | 203 | navigationTitle | `Wallpapers` | 桌布 |  |
| `tendies.n-items` | 294 | Text | `\(item.descriptorCount) item\(item.descriptorCount == 1 ? "" : "s")` | \(item.descriptorCount) 個項目\(item.descriptorCount == 1 ? "" : "s") | ternary item/items |
| `tendies.information` | 347 | Section | `Information` | 資訊 |  |
| `tendies.name` | 348 | disclosureTitle | `Name` | 名稱 |  |
| `tendies.file-name` | 349 | disclosureTitle | `File Name` | 檔案名稱 |  |
| `tendies.type` | 350 | disclosureTitle | `Type` | 類型 |  |
| `tendies.descriptors` | 351 | disclosureTitle | `Descriptors` | Descriptors |  |
| `tendies.target-extension` | 352 | disclosureTitle | `Target Extension` | 目標延伸功能 |  |
| `tendies.app-container` | 353 | disclosureTitle | `App Container` | App 容器 |  |
| `tendies.descriptor-archive` | 353 | disclosureTitle | `Descriptor Archive` | Descriptor 封存檔 |  |
| `tendies.format` | 353 | disclosureTitle | `Format` | 格式 |  |
| `tendies.contains-sqlite-database` | 355 | disclosureTitle | `Contains SQLite database` | 包含 SQLite 資料庫 |  |
| `tendies.warning` | 355 | disclosureTitle | `Warning` | 警告 |  |
| `tendies.done` | 363 | Button | `Done` | 完成 |  |

---

## README.md blocks

Translate headings + body prose. Keep code fences, URLs, badge image URLs, crypto addresses, and file-tree paths unchanged. Product name `AirCard-iOS` stays in headings where it is the project name.

### Block `readme.01.aircard-ios`

- **id:** `readme.01.aircard-ios`
- **file:** `README.md`
- **level:** h1
- **heading (EN):** AirCard-iOS
- **zh-Hant heading:** AirCard-iOS
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

**zh-Hant body:**

```markdown
<p align="center">
  <img src="ios-app/Assets.xcassets/AppIcon.appiconset/AppIcon.png" width="128" height="128" alt="AirCard-iOS Icon" style="border-radius: 28px; box-shadow: 0 8px 24px rgba(0,0,0,0.18);" />
</p>

<p align="center">
  直接在 iOS 27+ 上套用 Apple Wallet 卡片外觀、鎖定畫面密碼主題，以及 PosterBoard 桌布。
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-iOS%2027+-blue?style=flat-square&logo=apple" alt="Platform" />
  <img src="https://img.shields.io/badge/Swift-5.0-orange?style=flat-square&logo=swift" alt="Swift" />
  <img src="https://img.shields.io/badge/Rust-FFI%20Core-red?style=flat-square&logo=rust" alt="Rust" />
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" alt="License" />
  <a href="https://www.paypal.com/donate/?hosted_button_id=98QRTC2HFRA4Y"><img src="https://img.shields.io/badge/Donate-PayPal-00457C?style=flat-square&logo=paypal" alt="Donate with PayPal" /></a>
</p>
```


---

### Block `readme.02.overview`

- **id:** `readme.02.overview`
- **file:** `README.md`
- **level:** h2
- **heading (EN):** Overview
- **zh-Hant heading:** 概覽
- **notes:** README section

**English body:**

```markdown
AirCard-iOS customizes Apple Wallet card artwork, lock screen passcode dialers, and lock screen wallpapers on device without a jailbreak.

The app communicates with internal system services over a local loopback tunnel (`10.7.0.1` or `127.0.0.1`) provided by LocalDevVPN. File operations are handled by `AirliftFFI`, a Rust library that interfaces with the AirTraffic service.

> **Compatibility**: AirCard-iOS currently requires **iOS 27.0 or newer (iOS 27+)**.
```

**zh-Hant body:**

```markdown
AirCard-iOS 可在無需越獄的情況下，於裝置上自訂 Apple Wallet 卡片圖稿、鎖定畫面密碼撥號鍵盤，以及鎖定畫面桌布。

App 透過 LocalDevVPN 提供的本機 loopback 通道（`10.7.0.1` 或 `127.0.0.1`）與內部系統服務通訊。檔案操作由 `AirliftFFI` 處理，這是一個與 AirTraffic 服務介接的 Rust 函式庫。

> **相容性**：AirCard-iOS 目前需要 **iOS 27.0 或更新版本（iOS 27+）**。
```


---

### Block `readme.03.features`

- **id:** `readme.03.features`
- **file:** `README.md`
- **level:** h2
- **heading (EN):** Features
- **zh-Hant heading:** 功能
- **notes:** README section

**English body:**

```markdown

```

**zh-Hant body:**

```markdown

```


---

### Block `readme.04.apple-wallet-card-skins`

- **id:** `readme.04.apple-wallet-card-skins`
- **file:** `README.md`
- **level:** h3
- **heading (EN):** Apple Wallet card skins
- **zh-Hant heading:** Apple Wallet 卡片外觀
- **notes:** README section

**English body:**

```markdown
- Writes custom card artwork to Passbook caches (`cardBackgroundCombined@3x.png`, `@2x.png`, and `cardBackgroundCombined.pdf` for transit cards like Suica).
- Flushes front-face and thumbnail caches so new artwork appears immediately when Wallet opens.
- Detects card identifiers in real time when you bring up Apple Pay.
- Apply artwork to individual cards or batch-flash every detected card.
```

**zh-Hant body:**

```markdown
- 將自訂卡片圖稿寫入 Passbook 快取（`cardBackgroundCombined@3x.png`、`@2x.png`，以及交通卡如 Suica 使用的 `cardBackgroundCombined.pdf`）。
- 清除正面與縮圖快取，讓 Wallet 開啟時立即顯示新圖稿。
- 當你叫出 Apple Pay 時即時偵測卡片識別碼。
- 可為個別卡片套用圖稿，或批次刷寫所有已偵測到的卡片。
```


---

### Block `readme.05.passcode-dialer-themes`

- **id:** `readme.05.passcode-dialer-themes`
- **file:** `README.md`
- **level:** h3
- **heading (EN):** Passcode dialer themes
- **zh-Hant heading:** 密碼撥號鍵盤主題
- **notes:** README section

**English body:**

```markdown
- Live dialer preview with touch panning and zoom framing.
- Full poster layout across all ten buttons, or individual circular button cutouts.
- Targets system dialer caches (`TelephonyUI-10`).
- Localized number subtext options, including Ukrainian and Russian Cyrillic layouts.
- Import and export themes as `.passthm` files.
```

**zh-Hant body:**

```markdown
- 即時撥號鍵盤預覽，支援觸控平移與縮放構圖。
- 可將完整海報版面套用到全部十個按鍵，或裁切成個別圓形按鈕。
- 目標為系統撥號鍵盤快取（`TelephonyUI-10`）。
- 提供本地化數字副標選項，包含烏克蘭文與俄文西里爾字母版面。
- 可匯入／匯出 `.passthm` 主題檔。
```


---

### Block `readme.06.posterboard-wallpapers-tendies`

- **id:** `readme.06.posterboard-wallpapers-tendies`
- **file:** `README.md`
- **level:** h3
- **heading (EN):** PosterBoard wallpapers (.tendies)
- **zh-Hant heading:** PosterBoard 桌布（.tendies）
- **notes:** README section

**English body:**

```markdown
- Import and unpack `.tendies` wallpaper archives directly from the Files app.
- Auto-detects PosterBoard wallpaper containers and active descriptor UUIDs.
- Injects wallpaper configurations and assets into PosterBoard storage.
- Automatically triggers a NeoSpring respring after flashing to apply wallpapers without rebooting your iPhone.
```

**zh-Hant body:**

```markdown
- 直接從「檔案」App 匯入並解包 `.tendies` 桌布封存檔。
- 自動偵測 PosterBoard 桌布容器與作用中的 descriptor UUID。
- 將桌布設定與資源注入到 PosterBoard 儲存空間。
- 刷寫後自動觸發 NeoSpring 重新載入 SpringBoard，無需重新開機即可套用桌布。
```


---

### Block `readme.07.on-device-pairing`

- **id:** `readme.07.on-device-pairing`
- **file:** `README.md`
- **level:** h3
- **heading (EN):** On-device pairing
- **zh-Hant heading:** 裝置內配對
- **notes:** README section

**English body:**

```markdown
- Advertises locally over Bonjour so the phone can pair with itself via Settings > Privacy & Security > Developer Mode > Pair with AirCard-iOS.
- Reads and syncs pairing records automatically into `aircard_pairing.plist`.
- Once paired, no computer or external connection is needed.
```

**zh-Hant body:**

```markdown
- 透過 Bonjour 在本機廣播，讓手機能在設定 > 隱私權與安全性 > 開發人員模式 > Pair with AirCard-iOS 與自身配對。
- 自動讀取並同步配對紀錄到 `aircard_pairing.plist`。
- 配對完成後，不需要電腦或外部連線。
```


---

### Block `readme.08.prerequisites`

- **id:** `readme.08.prerequisites`
- **file:** `README.md`
- **level:** h2
- **heading (EN):** Prerequisites
- **zh-Hant heading:** 先決條件
- **notes:** README section

**English body:**

```markdown
1. **iOS 27+**: The exploit and paths currently target iOS 27.0 and above.
2. **LocalDevVPN**: Running in loopback mode (`10.7.0.1` or `127.0.0.1`) so local connections can reach internal device services.
3. **Developer Mode pairing**: Pair directly in Settings > Privacy & Security > Developer Mode > Pair with AirCard-iOS, or place an existing pairing plist in the app's documents directory.
```

**zh-Hant body:**

```markdown
1. **iOS 27+**：目前的 exploit 與路徑以 iOS 27.0 及以上為目標。
2. **LocalDevVPN**：以 loopback 模式執行（`10.7.0.1` 或 `127.0.0.1`），讓本機連線可到達內部裝置服務。
3. **開發人員模式配對**：直接在設定 > 隱私權與安全性 > 開發人員模式 > Pair with AirCard-iOS 配對，或將既有配對 plist 放到 App 的文件目錄。
```


---

### Block `readme.09.installation`

- **id:** `readme.09.installation`
- **file:** `README.md`
- **level:** h2
- **heading (EN):** Installation
- **zh-Hant heading:** 安裝
- **notes:** README section

**English body:**

```markdown
Install `AirCard-iOS.ipa` using your preferred sideloading method:

- SideStore or AltStore
- TrollStore
- LiveContainer
- Xcode or iOS App Signer
```

**zh-Hant body:**

```markdown
使用你偏好的側載方式安裝 `AirCard-iOS.ipa`：

- SideStore 或 AltStore
- TrollStore
- LiveContainer
- Xcode 或 iOS App Signer
```


---

### Block `readme.10.building-from-source`

- **id:** `readme.10.building-from-source`
- **file:** `README.md`
- **level:** h2
- **heading (EN):** Building from source
- **zh-Hant heading:** 從原始碼建置
- **notes:** README section

**English body:**

```markdown

```

**zh-Hant body:**

```markdown

```


---

### Block `readme.11.requirements`

- **id:** `readme.11.requirements`
- **file:** `README.md`
- **level:** h3
- **heading (EN):** Requirements
- **zh-Hant heading:** 需求
- **notes:** README section

**English body:**

```markdown
- macOS 14.0 or newer with Xcode 16 or newer
- XcodeGen (`brew install xcodegen`)
- Rust toolchain (only needed if rebuilding `rust-core`)
```

**zh-Hant body:**

```markdown
- macOS 14.0 或更新版本，且安裝 Xcode 16 或更新版本
- XcodeGen（`brew install xcodegen`）
- Rust 工具鏈（僅在重新建置 `rust-core` 時需要）
```


---

### Block `readme.12.build-the-ipa`

- **id:** `readme.12.build-the-ipa`
- **file:** `README.md`
- **level:** h3
- **heading (EN):** Build the IPA
- **zh-Hant heading:** 建置 IPA
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

**zh-Hant body:**

```markdown
```bash
git clone https://github.com/mak5er/AirCard-iOS.git
cd AirCard-iOS
./build-ipa.sh
```

完成的套件會寫入 `build/AirCard-iOS.ipa`。
```


---

### Block `readme.13.rebuilding-the-rust-framework`

- **id:** `readme.13.rebuilding-the-rust-framework`
- **file:** `README.md`
- **level:** h3
- **heading (EN):** Rebuilding the Rust framework
- **zh-Hant heading:** 重新建置 Rust framework
- **notes:** README section

**English body:**

```markdown
To compile changes in `rust-core`:
```bash
./build-ios.sh
```
```

**zh-Hant body:**

```markdown
若要編譯 `rust-core` 的變更：
```bash
./build-ios.sh
```
```


---

### Block `readme.14.repository-structure`

- **id:** `readme.14.repository-structure`
- **file:** `README.md`
- **level:** h2
- **heading (EN):** Repository structure
- **zh-Hant heading:** 儲存庫結構
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

**zh-Hant body:**

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


---

### Block `readme.15.credits`

- **id:** `readme.15.credits`
- **file:** `README.md`
- **level:** h2
- **heading (EN):** Credits
- **zh-Hant heading:** 致謝
- **notes:** README section

**English body:**

```markdown
- **[@mak5er](https://github.com/mak5er)**: Lead developer, UI, passcode theming, Tendies engine, on-device pairing.
- **[@merybist](https://github.com/merybist)**: Initial base port.
- **[AirLift](https://github.com/0xjohnnydev/airlift)** by **[0xjohnny (@0xjohnnydev)](https://github.com/0xjohnnydev)**: AirTraffic and ATAirlock sandbox escape research underlying `AirliftFFI`.
- **[NeoSpring](https://github.com/rooootdev/neospring)**: Swift implementation by **[@skadz108](https://github.com/skadz108)** and **[@rooootdev](https://github.com/rooootdev)**, and **[@neonmodder123](https://github.com/neonmodder123)** for the WebKit GPU process respring technique.
- Built upon concepts from the **AirCard** project.
```

**zh-Hant body:**

```markdown
- **[@mak5er](https://github.com/mak5er)**：主導開發者，UI、密碼主題、Tendies 引擎、裝置內配對。
- **[@merybist](https://github.com/merybist)**：初始基礎移植。
- **[AirLift](https://github.com/0xjohnnydev/airlift)** by **[0xjohnny (@0xjohnnydev)](https://github.com/0xjohnnydev)**：作為 `AirliftFFI` 基礎的 AirTraffic 與 ATAirlock 沙盒逃逸研究。
- **[NeoSpring](https://github.com/rooootdev/neospring)**：Swift 實作由 **[@skadz108](https://github.com/skadz108)** 與 **[@rooootdev](https://github.com/rooootdev)**，以及 **[@neonmodder123](https://github.com/neonmodder123)** 的 WebKit GPU process 重新載入 SpringBoard 技術。
- 建基於 **AirCard** 專案的概念。
```


---

### Block `readme.16.support`

- **id:** `readme.16.support`
- **file:** `README.md`
- **level:** h2
- **heading (EN):** Support
- **zh-Hant heading:** 支持專案
- **notes:** README section

**English body:**

```markdown
If you want to support AirCard-iOS development:

- **PayPal**: [Donate via PayPal](https://www.paypal.com/donate/?hosted_button_id=98QRTC2HFRA4Y)
- **TON**: `UQBm9KPhtMw-XVVjirUoa09wzrlyWsbeZhKfefl1Uw-qNZ-r`
- **USDT (TRC20)**: `TDkDMCyjYxgvkWUnQiF5Erk2RyPQMT6G1n`
- **USDT / BNB (BEP20)**: `0x0954dc491c502849d04956ef74634aa5931a08e8`
```

**zh-Hant body:**

```markdown
若想支持 AirCard-iOS 的開發：

- **PayPal**：[透過 PayPal 贊助](https://www.paypal.com/donate/?hosted_button_id=98QRTC2HFRA4Y)
- **TON**：`UQBm9KPhtMw-XVVjirUoa09wzrlyWsbeZhKfefl1Uw-qNZ-r`
- **USDT (TRC20)**：`TDkDMCyjYxgvkWUnQiF5Erk2RyPQMT6G1n`
- **USDT / BNB (BEP20)**：`0x0954dc491c502849d04956ef74634aa5931a08e8`
```


---

### Block `readme.17.license`

- **id:** `readme.17.license`
- **file:** `README.md`
- **level:** h2
- **heading (EN):** License
- **zh-Hant heading:** 授權條款
- **notes:** README section

**English body:**

```markdown
MIT License. See [LICENSE](LICENSE) for details.
```

**zh-Hant body:**

```markdown
MIT License。詳見 [LICENSE](LICENSE)。
```


---
