# AirCard-iOS 繁體中文版

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
  <img src="https://img.shields.io/badge/介面語言-繁體中文-brightgreen?style=flat-square" alt="繁體中文" />
  <a href="https://www.paypal.com/donate/?hosted_button_id=98QRTC2HFRA4Y"><img src="https://img.shields.io/badge/Donate-PayPal-00457C?style=flat-square&logo=paypal" alt="Donate with PayPal" /></a>
</p>

## 關於本倉庫

本倉庫是 [Mak5er/AirCard-iOS](https://github.com/Mak5er/AirCard-iOS) 的**繁體中文**版，由 Vik1n9 維護。介面文案自原版英文重寫為正體中文。

應用顯示名稱仍維持 `AirCard-iOS`（Bonjour 配對服務名，勿改）。

## 概覽

AirCard-iOS 可在無需越獄的情況下，於裝置上自訂 Apple Wallet 卡片圖稿、鎖定畫面密碼撥號鍵盤，以及鎖定畫面桌布。

App 透過 LocalDevVPN 提供的本機 loopback 通道（`10.7.0.1` 或 `127.0.0.1`）與內部系統服務通訊。檔案操作由 `AirliftFFI` 處理，這是一個與 AirTraffic 服務介接的 Rust 函式庫。

> **相容性**：AirCard-iOS 目前需要 **iOS 27.0 或更新版本（iOS 27+）**。

## 功能

### Apple Wallet 卡片外觀
- 將自訂卡片圖稿寫入 Passbook 快取（`cardBackgroundCombined@3x.png`、`@2x.png`，以及交通卡如 Suica 使用的 `cardBackgroundCombined.pdf`）。
- 清除正面與縮圖快取，讓 Wallet 開啟時立即顯示新圖稿。
- 當你叫出 Apple Pay 時即時偵測卡片識別碼。
- 可為個別卡片套用圖稿，或批次刷寫所有已偵測到的卡片。

### 密碼撥號鍵盤主題
- 即時撥號鍵盤預覽，支援觸控平移與縮放構圖。
- 可將完整海報版面套用到全部十個按鍵，或裁切成個別圓形按鈕。
- 目標為系統撥號鍵盤快取（`TelephonyUI-10`）。
- 提供本地化數字副標選項，包含烏克蘭文與俄文西里爾字母版面。
- 可匯入／匯出 `.passthm` 主題檔。

### PosterBoard 桌布（.tendies）
- 直接從「檔案」App 匯入並解包 `.tendies` 桌布封存檔。
- 自動偵測 PosterBoard 桌布容器與作用中的 descriptor UUID。
- 將桌布設定與資源注入到 PosterBoard 儲存空間。
- 刷寫後自動觸發 NeoSpring 重新載入 SpringBoard，無需重新開機即可套用桌布。

### 裝置內配對
- 透過 Bonjour 在本機廣播，讓手機能在設定 > 隱私權與安全性 > 開發人員模式 > Pair with AirCard-iOS 與自身配對。
- 自動讀取並同步配對紀錄到 `aircard_pairing.plist`。
- 配對完成後，不需要電腦或外部連線。

## 先決條件

1. **iOS 27+**：目前的 exploit 與路徑以 iOS 27.0 及以上為目標。
2. **LocalDevVPN**：以 loopback 模式執行（`10.7.0.1` 或 `127.0.0.1`），讓本機連線可到達內部裝置服務。
3. **開發人員模式配對**：直接在設定 > 隱私權與安全性 > 開發人員模式 > Pair with AirCard-iOS 配對，或將既有配對 plist 放到 App 的文件目錄。

## 安裝

使用你偏好的側載方式安裝 `AirCard-iOS.ipa`：

- SideStore 或 AltStore
- TrollStore
- LiveContainer
- Xcode 或 iOS App Signer

## 從原始碼建置

### 需求
- macOS 14.0 或更新版本，且安裝 Xcode 16 或更新版本
- XcodeGen（`brew install xcodegen`）
- Rust 工具鏈（僅在重新建置 `rust-core` 時需要）

### 建置 IPA
```bash
git clone https://github.com/Vik1n9/AirCard-iOS-TW.git
cd AirCard-iOS-TW
./build-ipa.sh
```

完成的套件會寫入 `build/AirCard-iOS.ipa`。

### 重新建置 Rust framework
若要編譯 `rust-core` 的變更：
```bash
./build-ios.sh
```

## 儲存庫結構

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

## 致謝

- **[@mak5er](https://github.com/mak5er)**：主導開發者，UI、密碼主題、Tendies 引擎、裝置內配對。
- **[@merybist](https://github.com/merybist)**：初始基礎移植。
- **[AirLift](https://github.com/0xjohnnydev/airlift)** by **[0xjohnny (@0xjohnnydev)](https://github.com/0xjohnnydev)**：作為 `AirliftFFI` 基礎的 AirTraffic 與 ATAirlock 沙盒逃逸研究。
- **[NeoSpring](https://github.com/rooootdev/neospring)**：Swift 實作由 **[@skadz108](https://github.com/skadz108)** 與 **[@rooootdev](https://github.com/rooootdev)**，以及 **[@neonmodder123](https://github.com/neonmodder123)** 的 WebKit GPU process 重新載入 SpringBoard 技術。
- 建基於 **AirCard** 專案的概念。

## 支持專案

若想支持 AirCard-iOS 的開發：

- **PayPal**：[透過 PayPal 贊助](https://www.paypal.com/donate/?hosted_button_id=98QRTC2HFRA4Y)
- **TON**：`UQBm9KPhtMw-XVVjirUoa09wzrlyWsbeZhKfefl1Uw-qNZ-r`
- **USDT (TRC20)**：`TDkDMCyjYxgvkWUnQiF5Erk2RyPQMT6G1n`
- **USDT / BNB (BEP20)**：`0x0954dc491c502849d04956ef74634aa5931a08e8`

## 授權條款

MIT License。詳見 [LICENSE](LICENSE)。

---

上游專案：[Mak5er/AirCard-iOS](https://github.com/Mak5er/AirCard-iOS)
