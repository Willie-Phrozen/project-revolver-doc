# Klipper UI 圖片細部 UI 元件拆解對照表

本文件針對 Klipper 後台頁面截圖，進行了深度的 UI 元件拆解，將每一張圖片中肉眼可見的「按鈕名稱」、「輸入欄位」、「標籤文字」及「下拉選單」等細部功能逐一列出，方便在實作 C++ Native UI 時對齊細節。

> **📝 優先度與功能等級填寫說明**
> 請在各細項功能開頭的方括弧 `[   ,   ]` 內填入對應的代碼，以利後續開發評估：
> 
> **優先度 (Priority) 評定基準：**
> * **`P0`**: 這版非做不可
> * **`P1`**: 重要，但可延後
> * **`P2`**: 有空再說
> * **`Drop`**: 不打算做
>
> **功能等級 (Level) 分類：**
> * **`A`**: 基本要顯示的功能
> * **`A+`**: 進階功能
> 
> *(例如：`[ P0, A ]` 代表核心必做，`[ Drop, A+ ]` 代表放棄此進階功能)*

---

### 1. 就緒狀態與歷史記錄 [P1,A+] 
* <span style="background-color:#0000ff">Note. 因內存不夠，歷史紀錄可能會跳動變得不準(跟著USB跑 非機台歷史)</span>

<table>
<tr>
<td style="vertical-align: top; width: 520px;">
<img src="./images/Screenshot%202026-04-06%20111955.png" width="500">
</td>
<td style="vertical-align: top; padding-left: 16px;">

* **面板標題區：**
  * [   ,   ] **功能: 重新打印**
* **清單標題列：** 
  * [   ,   ] 檔案名稱 (例如 `3方塊.gcode`)
  * [   ,   ] 列印狀態圖示 (例如圖中的取消/禁止圓圈圖示)
  * [   ,   ] 列印歷時 (例如 `5m 8s`、`13m 48s`)

</td>
</tr>
</table>

### 2. 攝影機多重預覽監控 [P0,A]
<table>
<tr>
<td style="vertical-align: top; width: 520px;">
<img src="./images/Screenshot%202026-04-06%20112032.png" width="500">
</td>
<td style="vertical-align: top; padding-left: 16px;">

* **面板標題區：**
  * [ X ,  ] `切換相機` 不會支援多個攝影機
  * [ P0 , A ] `Setting` (垂直水平翻轉設定)
  * [ P0 , A ] `Camera Switch` (開關 camera)
  * [ P0 , A ] `Light Switch` (開關機台燈)
* **視訊畫面附掛元件：**
  * [ P2 ,   ] 右上角：`『 』` (全螢幕展開按鈕)
  * [ P2 ,   ] 左下角：攝影機名稱標籤浮水印 (`my_cam0`、`my_cam1`)
  * [ P2 ,   ] 右下角：FPS 標籤浮水印 (`fps: 00`、`fps: 01`)
* [ X ,   ] **多Camera設置：**

</td>
</tr>
</table>

### 3. 移動與擠出綜合控制面板
<table>
<tr>
<td style="vertical-align: top; width: 520px;">
<img src="./images/Screenshot%202026-04-06%20112051.png" width="500">
</td>
<td style="vertical-align: top; padding-left: 16px;">

* **面板標題區：**
  * [  ,  ] **擠出警告圖示(未滿170)** `驚嘆號齒輪`
  * [  ,  ] **FORCE_MOVE** 
  * [  ,  ] **關閉電機** 
  * **工具** 
    * [  ,  ] **MANUAL_PROBE** 
    * [  ,  ] **PROBE_CALIBRATE** 
* **左半部 - 控制區域與巨集操作**
  * [   ,   ] **T0~T15切換紐** `上方 T0 到 T15 排列的方形按鈕`
  * [ P1 , A ] **XYZ 軸向移動按鈕：** `↑`、`↓`、`←`、`→`
  * [ P1 , A ] **歸位按鈕：** 🏠 `全部歸位`、🏠 `歸位X`、🏠 `歸位Y` 及方向鍵中央的單獨 🏠 圖標
  * [ P1 , A ] **移動距離選擇紐：** `0.1`、`1`、`10`、`25`、`50`、`100` (負責決定點動的毫米數)
  * **自訂巨集按鈕 (藍底/灰底圖示)：
    * [   ,   ] **`AMS-P28-CONNECT`**
    * [   ,   ] **`P4-STOP`**
    * [   ,   ] **`↓T1....→P114`** 
    * [   ,   ] **`PRZ_RESUME`** 
    * [   ,   ] **`PRZ_CANCEL`** 
    * [   ,   ] **`PRZ_PAUSE__`** 
    * [   ,   ] **`PRZ_ADC____`** 

* **右半部 - 座標與擠出操作：**
  * [   ,   ] **座標顯示與手動輸入框：** `X`、`Y` 軸與 `Z` 軸數值框
  * [   ,   ] **座標切換紐：** 絕對座標/相對座標
  * **擠出設定：**
    * [   ,   ] **擠出設定：** `擠出距離` 輸入框 (`10 mm`)、`擠出速度` 輸入框 (`5 mm/s`)
    * [   ,   ] **出料控制按鈕：** `回抽`、`擠出`
  * [   ,   ] **平台Offset操作功能：** `包含偏移量, 上下位移紐, Z軸偏移量提示`

* **下半部 - 切片參數全局倍率調整：**
  * [ X ,   ] **狀態文字：** `~ 191.4 mm @ 12 mm³/s, 168 mm/s`包含簡要和詳細(展開的話)
  * [ P1 , A+ ] **移動速度** (帶 `↺` 復原鈕、`100 %` 文字輸入框、底下為滑動條 Slider)
  * [ P2 , A+ ] **擠出流量** (帶 `↺` 復原鈕、`100 %` 文字輸入框、底下為滑動條 Slider)
  * [ X ,   ] **壓力補償** (帶 `↺` 復原鈕、`0.032 s` 文字輸入框、底下為滑動條 Slider)
  * [ X ,   ] **平滑時間** (帶 `↺` 復原鈕、`0.03 s` 文字輸入框、底下為滑動條 Slider)

</td>
</tr>
</table>

### 4. 溫度監測與動態折線圖
<table>
<tr>
<td style="vertical-align: top; width: 520px;">
<img src="./images/Screenshot%202026-04-06%20112145.png" width="500">
</td>
<td style="vertical-align: top; padding-left: 16px;">

* [ P0 , A ] **面板標題區：** `溫度`、`?` (幫助提示鈕)
* [ P0 , A ] **頂部按鈕：** `火苗 預設 v` (Profile下拉選單)、`設定齒輪`、`^` (面板折疊)
* [ P0 , A ] **清單標題列：** `名稱`、`功率`、`變化值`、`當前值`、`目標值`
* [ P0 , A ] **感測器列表行：**
  * [ P0 , A ] `Extruder` (帶紅色火苗圖示、`off` 標籤、`+0.0°c/s` 變化量、當前讀數 `36.9°C` / 輸入框 `0 °C`)
  * [ P0 , A ] `Heater Bed` (帶藍色火苗圖示，其餘元素同上)
  * [ P0 , A ] `Chamber Sensor` (帶溫度計圖示，僅顯示讀數無目標框)
* [ P0 , A ] **圖表區塊：** Y軸 `Temperature °C`，X軸 `時間刻度`。

</td>
</tr>
</table>

### 5. 終端機與命令控制台
<table>
<tr>
<td style="vertical-align: top; width: 520px;">
<img src="./images/Screenshot%202026-04-06%20112153.png" width="500">
</td>
<td style="vertical-align: top; padding-left: 16px;">

* **面板標題區：**
  * [ P1 , A+ ] **頂部工具列：** `↓` (跳至最新行)、`『 』` (視窗最大化/展開)、`🗑️` (清空畫面)、`設定齒輪`、`^`
* [ P1 , A+ ] **對話輸出區：** 以等寬字體輸出的 Log 訊息列 (如 `// self.G_AutoReplace...`)
* **底部控制區：**
  * [ P1 , A+ ] G-Code 空白文字輸入方塊
  * [ P1 , A+ ] **指令快捷按鈕：** `SEND`、`P28`、`P114`、`ADC`、`PAUSE`、`RESUME`、`CANCEL`、`STOP`

</td>
</tr>
</table>

### 6. 內置任務/儲存檔案總管 
* <span style="background-color:#0000ff"> 需要一些事情確認 </span>
  * <span style="background-color:#0000ff"> 有Local 和 USB 之分 </span>
  * <span style="background-color:#0000ff"> Local 可能需要傳機台後砍檔功能以節省空間 </span>
  * <span style="background-color:#0000ff"> USB插拔防呆 </span>

<table>
<tr>
<td style="vertical-align: top; width: 520px;">
<img src="./images/Screenshot%202026-04-06%20112201.png" width="500">
</td>
<td style="vertical-align: top; padding-left: 16px;">

* **工具篩選列：**
  * [ P0 , A ] 路徑列 `/` (返回上層)
  * [  ,  ] `Thumbnail 縮放`
  * [  ,  ] `Select columns` 勾選要顯示哪些property
  * [  ,  ] `Go to File` 出現較大的視窗過目當前的所有檔案
  * [  ,  ] `過濾` 例如隱藏已印過項目或被隱藏的項目
  * [  ,  ] `添加` 上傳文件、上傳資料夾、上傳並打印、新建文件、新建目錄
  * [  ,  ] `刷新`
  * [  ,  ] `搜尋欄`
* **任務列表內容** 
* [ P0 , A ] `名稱`、`上次打印時間`、`修改時間 ↓`、`文件大小`...等，以及其他property
* [ P0 , A ] **縮圖** `.tmp` 資料夾圖示、`USB` 資料夾圖示、及 `.gcode` 的檔案清單。

</td>
</tr>
</table>

### 7. 特殊風扇與輸出針腳控制
<table>
<tr>
<td style="vertical-align: top; width: 520px;">
<img src="./images/Screenshot%202026-04-06%20112241.png" width="500">
</td>
<td style="vertical-align: top; padding-left: 16px;">

* **控制區塊 (左側風扇)：**
  * [ P0 , A ] `Part Fan` (帶 `↺` 復原鈕、`0 %` 輸入框、滑桿)
  * [ P2 , A ] `Chamber Fan` (帶 `↺` 復原鈕、`0 %` 輸入框、滑桿)
  * [ P2 , A ] `Cooling Fan` (帶 `↺` 復原鈕、`0 %` 輸入框、滑桿)
  * [ X ,   ] 獨立純文字列 `Fan 0` / `關閉`
* [ X ,   ] **控制區塊 (右側針腳/系統扇)：**
  * [ X ,   ] `Probe Pin` (附帶一個 Switch 滑動開關按鈕)
  * [ X ,   ] `Board Fan` (附帶一個 Switch 滑動開關按鈕)
  * [ X ,   ] `Fan Assist` (帶 `↺` 復原鈕、`0` 數值輸入框、滑桿)

</td>
</tr>
</table>

### 8. 打印機動態限制調整
<table>
<tr>
<td style="vertical-align: top; width: 520px;">
<img src="./images/Screenshot%202026-04-06%20112246.png" width="500">
</td>
<td style="vertical-align: top; padding-left: 16px;">

* **參數控制區 (皆配有 `↺` 復原鈕、數值輸入框、滑桿元件)：**
  * [ P2 , A ] `速度` (`1000 mm/s`)
  * [ P2 , A ] `加速度` (`10000 mm/s²`)
  * [ P2 , A ] `轉角速度` (`9 mm/s`)
  * [ P2 , A ] `加速到減速度` (`5000 mm/s²`)

</td>
</tr>
</table>

### 9. 即時 G-code 圖層解碼檢視
* <span style="background-color:#0000ff"> 注意事項 </span>
  * <span style="background-color:#0000ff"> 基本功能要看小龍門面板有放才做 </span>

<table>
<tr>
<td style="vertical-align: top; width: 520px;">
<img src="./images/Screenshot%202026-04-06%20112257.png" width="500">
</td>
<td style="vertical-align: top; padding-left: 16px;">

* [ P2 , A ] **面板標題區：** `載入當前文件, 放大視窗`
* [ P2 , A ] **進度控制區：**
  * [ P2 , A ] `當前層數` 取值標籤 (帶有含游標的拉桿，以及 `0` 的數值框)
  * [ P2 , A ] `當前進度` 取值標籤 (帶有含游標的拉桿，以及 `0` 的數值框)
* [ P2 , A ] **右側資訊與操作區：**
  * [ P2 , A ] `總層數`, `0`
  * [ P2 , A ] `當前層高`, `0`
  * [ P2 , A ] `重置文件` (按鈕)
* [ P2 , A ] **可視畫布區：** 佔據絕大版面的 2D 座標機台格線區域。

</td>
</tr>
</table>

### 10. 熱床網格補償(Bed Mesh)曲面視覺化
<table>
<tr>
<td style="vertical-align: top; width: 520px;">
<img src="./images/Screenshot%202026-04-06%20112305.png" width="500">
</td>
<td style="vertical-align: top; padding-left: 16px;">

* [ P1 , A ] **`校準`**  頂部右側按鈕
* [ P1 , A ] **圖表區附帶文字組件：** 總之畫面內有的就要保留
  * [ P1 , A ] 標註文字：左側 `0.7113` (最高)、左側 `-0.3875` (最低)、右上 `Range: 0.8987` (最大公差)
  * [ P1 , A ] `X`, `Y`, `Z` 三軸的數值刻度標籤文字
  * [ P1 , A ] 色譜圖例 (ColorBar) 與居中的 3D 渲染圖表本身

</td>
</tr>
</table>

### 11. 系統設定與腳本文件編修
* <span style="background-color:#0000ff"> config 會放在USB 還是 local? </span>

<table>
<tr>
<td style="vertical-align: top; width: 520px;">
<img src="./images/Screenshot%202026-04-06%20112342.png" width="500">
</td>
<td style="vertical-align: top; padding-left: 16px;">

* [ P3 , A+ ] **預計此面板隱藏，優先度往後擺**
  * [  ,  ] **工具列元件：** 路徑文字 `/`、🔍搜尋圖示、漏斗、`+` 按鈕、`↺` 重新整理、搜尋輸入框
  * [  ,  ] **標題列表：** Checkbox (打勾方塊), `名稱`, `修改時間 ↓`, `文件大小`
  * [  ,  ] **文件項目：** `printer.cfg` 等檔案名稱文字，每一個最前面都有對應的 Checkbox (多選框)，以及文件圖標 `📄`

</td>
</tr>
</table>

### 12. 系統錯誤與執行日誌查核
* <span style="background-color:#0000ff"> 主要是客服會需要，他可以跟user拿資料後進行問題確認 </span>

<table>
<tr>
<td style="vertical-align: top; width: 520px;">
<img src="./images/Screenshot%202026-04-06%20112349.png" width="500">
</td>
<td style="vertical-align: top; padding-left: 16px;">

* [ X ,  ] **改用替代方案: 可以下載整個log即可(下一個面板的功能)，所以此頁捨棄**
  * [  ,  ] **面板標題區：** `其他文件（日志、文檔及參考配置）`
  * [  ,  ] **工具列：** 路徑 `/`、🔍、漏斗、`↺` 以及搜尋方塊
  * [  ,  ] **頁次切換元件 (Nav Tabs)：** `LOGS`、`DOCS`、`CONFIG_EXAMPLES` 三個文字頁籤按鈕
  * [  ,  ] **標題列表：** `名稱`, `修改時間 ↓`, `文件大小`
  * [  ,  ] **文件項目：** `moonraker.log` 等，每列最前面配有一張帶有下載箭頭的文件圖標 (無 Checkbox)

</td>
</tr>
</table>

### 13. 硬體與主機核心綜合資訊
<table>
<tr>
<td style="vertical-align: top; width: 520px;">
<img src="./images/Screenshot%202026-04-06%20112402.png" width="500">
</td>
<td style="vertical-align: top; padding-left: 16px;">

* [ P0 , A ] **系統狀態欄 (唯讀文字標籤)：**
  * `[  ,  ]` 屬性名：`主機名`、`內存`、`處理器描述`、`操作系統`、`發行版`、`開發代號`、`網路`
  * `[  ,  ]` 對應文字值：`mkspi`、`976.3 MB`、`wlan0 (192.168.30.44)` 等及紅色警示句 `# PLEASE DO NOT EDIT THIS FILE`
* **系統操作大按鈕列 (左鍵觸發)：**
  * `[ P0 , A ]` `重啟KLIPPER` (藍底按鈕)
  * `[ P0 , A ]` `重啟FIRMWARE` (藍底按鈕)
  * `[ P0 , A ]` `📥 KLIPPY.LOG` (灰底帶圖層的下載按鈕)
  * `[ P0 , A ]` `📥 MOONRAKER.LOG` (灰底帶圖層的下載按鈕)

</td>
</tr>
</table>

### 14. 機內磁碟與儲存容量檢查
<table>
<tr>
<td style="vertical-align: top; width: 520px;">
<img src="./images/Screenshot%202026-04-06%20112408.png" width="500">
</td>
<td style="vertical-align: top; padding-left: 16px;">

* [ P0 , A ] **圖表/文字元件**

</td>
</tr>
</table>
