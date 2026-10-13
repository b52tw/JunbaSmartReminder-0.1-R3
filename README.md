# Junba 智慧提醒 Android v0.1

Android 8+ 原生 Java 專案（測試目標：vivo V2413 / Android 16）。作者：峻爸。

## 功能
- 每次啟動或返回前景時重新查詢授權日曆、系統下一次鬧鐘與 App 記事排程
- 完整日曆帳號名稱 / 日曆篩選；唯讀展示 60 天內活動、提醒提前分鐘及 RRULE
- 新增、刪除記事及指定日期、時間、提前提醒；每日或每週重複
- Android 精確鬧鐘權限入口、通知權限與測試提醒
- 原廠時鐘開啟、公開 ACTION_SET_ALARM 建立請求（需使用者確認）
- Gemini API 金鑰臨時輸入與真實 HTTP 連線測試；不儲存金鑰

## 不支援 / 系統限制
- 無法取得或批次修改 vivo 所有原廠鬧鐘，亦無原廠稍後提醒次數
- 不保證裝置待機、省電管理情境的實際響鈴；需真機測試
- 不讀取語音助理歷史；僅讀取同步至手機的日曆
- v0.1 未加入自動把日曆活動轉成原廠鬧鐘，以防重複建立
- App 自有提醒使用高重要性通知，不是 vivo 原廠時鐘鈴聲

## 編譯
將此專案推到 GitHub，Actions → Build Android APK → Run workflow，完成後於 Artifacts 下載 `JunbaSmartReminder-debug-apk`。或安裝 Android Studio (JDK 17, Android SDK 35)，執行 `gradle assembleDebug`。Debug APK 僅供測試，發行版本需正式簽署。

## 驗收注意
允許「日曆／通知／精確鬧鐘」相關權限，並於 vivo 電池管理允許 App 後台運作。請用 1 分鐘測試提醒確認實際通知／聲音。原廠時鐘的新增與內容必須回到 vivo 時鐘人工核對。

## R3 修正版（2026-10-13）

GitHub Actions 的 R2 版卡在 `command -v sdkmanager`，因 SDK 工具存在於 `$ANDROID_HOME/cmdline-tools/<version>/bin/`，但未在 Runner 的 PATH 中。

R3 不再直接執行 `command -v sdkmanager`，而是在實際 Android SDK 資料夾中搜尋 `sdkmanager` 的絕對路徑。找到後接受授權，安裝 Android SDK 35 與 Build Tools 35.0.0，再用 Java 17／Gradle 8.10.2 執行 `assembleDebug`。

### 重跑方式
1. 解壓縮 R3 封包（ZIP 根目錄已是專案檔案，沒有額外包一層資料夾）。
2. 將裡面的 `.github`、`app`、`build.gradle`、`settings.gradle`、`gradle.properties` 與 README.md 上傳到 GitHub 專案**根目錄**（需要取代原檔）。
3. `Actions → Build Android APK → Run workflow`。成功後 Artifacts 應出現 `JunbaSmartReminder-v0.1-R3-debug-APK`。下載解壓後取得 `app-debug.apk`。

### 說明
- 本 ZIP 為完整可編譯原始碼與自動建置流程，**不是已完成的 APK**。只有當 GitHub Actions 成功後，才會產生 APK。
- Java 及 Android App 尚未通過 GitHub Actions 全流程編譯或 vivo V2413 真機驗收。
- 如果 GitHub Actions 仍失敗，請提供執行連結或執行 ID；可根據實際錯誤而不是猜測排查。
