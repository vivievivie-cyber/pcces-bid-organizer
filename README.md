# PCCES 標單整理助手

## GitHub Pages 部署檔

網站檔案已發布於 [`vivievivie-cyber/pcces-bid-organizer`](https://github.com/vivievivie-cyber/pcces-bid-organizer)：`index.html`、`juxiang-logo.png` 與本說明文件。`程式碼.gs` 是原 Apps Script 入口檔；純 GitHub Pages 不需要它。

GitHub Pages 需在儲存庫設定中啟用 `main` 分支的根目錄作為發布來源；現有 `vivievivie-cyber/-` 消防排煙網站未變更。

## 已整理的功能

- 僅接受真正的 PCCES `.xls`，輸出新 `.xlsx` 檔；會拒絕 `.xlsx` 或只改了副檔名的檔案。
- 執行前檢查檔案內容、`預算詳細表` 工作表及第 8 列 A:F 標題。
- 四個功能各自下載新檔，不修改上傳的來源檔。
- 第 1 至 7 列隱藏；第 8 列維持表頭；功能 4 的 I:P 標題放在第 8 列。
- 功能 3 保留小計、合計列及有金額的列；B 欄自動換行，並依瀏覽器量測字型及欄寬後計算所需列高。輸出不調整任何欄寬。
- 小計、合計、總計／總價列以不同底色反白，分別為淡黃、淡藍、淡綠。
- 所有工作表都嘗試解除工作表保護。
- 功能 4：D 保留預算數量；I=D；J 為廠商報價輸入；K=I×J；L 預設 1.2；M 預設 1.0；N=I×M；O=J×L 並回填 E；P=N×O。H 欄比對 F 與 P，不相等時以黃色標示；小計、合計列也計算 P 並納入比對。

## `.xls` 相容性說明

舊版 `.xls` 先用 SheetJS Community Edition 轉成 `.xlsx`，再以 ExcelJS 處理。舊格式的字型、框線、合併儲存格等外觀可能無法完整保留；正式使用前請抽查轉出的格式與列印版面。B 欄列高以瀏覽器 Canvas 根據儲存格字型與原欄寬估算，Excel 不同版本及字型替代可能有少量差異；欄寬保持來源設定。

工具在瀏覽器端讀取與處理檔案，不會將預算檔送到 Apps Script 伺服器；需要可連線載入 ExcelJS 與 SheetJS CDN。
