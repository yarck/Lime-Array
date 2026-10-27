# Lime-Array 修改說明

Lime-Array 是以 [萊姆輸入法 LIME HD](https://github.com/lime-ime/limeime)（v6.1.38）為基礎的分支版本，針對**行列輸入法**與**三星平板**使用情境調整外觀與操作。

- 套件名稱：`org.limeime.array`
- App 名稱：萊姆行列
- 可與原版萊姆輸入法同時安裝、並存使用（兩者資料不互通）

## 下載

[LimeArray APK（最新版）](https://github.com/yarck/Lime-Array/releases/download/latest/LimeArray202661380-v6.1.38.apk)

每次推送到 `main` 會由 GitHub Actions 自動編譯，並更新同一個下載連結。APK 使用固定簽章，新版可直接覆蓋安裝。

## 修改重點

### 1. 鍵盤外觀仿三星鍵盤

- **按鍵高度**：行列、英文、123 符號鍵盤統一縮為原本的約 87%，三種鍵盤切換時高度一致。
- **按鍵形狀**：圓角加大（3dp → 8dp），鍵與鍵之間的間隙加寬。
- **配色（淺色主題）**：淺灰底、白色字鍵、灰色功能鍵。
- **字樣配置**：主字（行列碼如「1⇡」、注音符號）放大置中；副字（英文字母）縮小放在按鍵右上角。

### 2. 選字方式改為 Windows 行列做法

- 輸入字根後按 **1–9、0** 直接選第 1–10 個候選字，螢幕鍵盤數字列與實體鍵盤皆適用。
- 候選列標示為 1、2、3…（原本是 `! @ #`）。
- 輸入框只有 `w` 時，數字視為字根，可用 w1–w0 打符號；進入符號表後同樣用數字選。
- 按到沒有對應候選字的數字會被忽略，不會混入字根。
- 實體鍵盤的 Shift+數字選字仍可使用。

### 3. 接上實體鍵盤時自動收起虛擬鍵盤

- 偵測到已連接的實體鍵盤（如三星書本式鍵盤皮套、藍牙鍵盤）時，虛擬鍵盤不展開，只保留最下方候選列。
- 候選列右側「展開鍵盤」按鈕旁顯示目前狀態：中文模式為「中・行列」（隨輸入法變動），英文模式為「英」。
- 需要時點展開鍵盤按鈕即可叫出完整虛擬鍵盤；換到下一個輸入框會自動收起。

## 相關檔案

| 項目 | 主要檔案 |
|---|---|
| 按鍵高度 | `res/values*/dimens.xml`（`array_key_height`）、`res/xml/lime_array*.xml`、`lime_english*.xml`、`lime_abc*.xml`、`lime_number*.xml`、`lime_num_sym2*.xml` |
| 按鍵形狀與配色 | `res/drawable/btn_flat_keyboard_*_light.xml`、`res/values/colors.xml` |
| 字樣配置 | `keyboard/LIMEKeyboardBaseView.java`（`SAMSUNG_KEY_STYLE`） |
| 數字選字 | `LIMEService.java`（`handleArrayDigitSelection`、`arrayDigitSelectionActive`） |
| 實體鍵盤與狀態列 | `LIMEService.java`（`isHardwareKeyboardAttached`、`getInputModeStatusLabel`）、`candidate/CandidateInInputViewContainer.java`、`res/layout/inputcandidate.xml` |
| 自動編譯 | `.github/workflows/build-apk.yml`、`app/signing/lime-array-debug.p12` |

（檔案路徑皆位於 `LimeStudio/app/src/main/` 下，自動編譯相關除外。）

## 授權

沿用原專案 GPL v3 授權。
