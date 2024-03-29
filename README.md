# 運用深度學習於圖書館人流監控

---

## 背景與動機

每日圖書館入館人次達兩千人，包括校內外讀者。為了應對眾多讀者，特別是處理不受歡迎的黑名單成員，我們引入深度學習技術提供三項功能：即時人流監控、閉館人流檢查，以及偵測特殊人士。這些功能可協助圖書館管理者有效掌握人流狀況，確保安全並提供愉悅的學習環境。

## 系統建置

在這個系統中，我們運用了 MTCNN 進行人臉檢測、DeepSORT 進行物件追蹤，以及 FaceNet 進行人臉特徵提取和人臉識別。系統的主要功能可以分為四個方向：監控、查詢、統計和設定。接下來將透過系統功能架構及系統架構詳細介紹本系統。

### 系統功能架構

本系統的主要功能分為四個方向：監控、查詢、統計和設定，詳細內容如下圖所示。

- **監控功能**：包括即時人流監控、閉館人流檢查和偵測特殊人士。透過攝影機進行即時人流監控，可以計算館內人數，同時偵測是否為特殊人士，若是則會寄送通知給圖書館管理者。在閉館時，系統會進行人流檢查，並顯示尚未離館的人員的照片和相關資料。
- **查詢功能**：允許根據特定條件進行查詢。可以按照時間段、ID、姓名、學號、員編或圖片進行查詢，查詢結果將顯示在右側的表格中。
- **統計功能**：根據設定的起訖日期和圖表類型（如長條圖或折線圖），繪製人數統計圖和人數趨勢分析圖。還提供匯出功能，支援 CSV、EXCEL、圖片（.jpg）和 PDF 格式。
- **設定功能**：包括管理特殊名單和通知名單。可以新增、修改和刪除特殊名單中的人員資料，以及新增、修改和刪除通知名單中的對象。
![Untitled](https://github.com/daisy00000/Pedestrian-flow-monitoring-Detections-in-Library-by-Using-Deep-Learning-Technology/assets/121708806/48573e3e-303e-4203-a7e0-8633e10eea42)

### 系統架構

系統架構將詳細介紹整個系統的架構流程。一旦啟動系統，即時監控影像將顯示在主畫面上。透過MTCNN進行人臉偵測，當有入館者被捕捉到時，系統將截取其臉部截圖，接著利用FaceNet進行特徵值提取，再透過DeepSort進行人臉追蹤。當人員離開館時，再次利用FaceNet進行人臉比對，以確認離館者在當日進館人員資料庫中的身分，隨後將其移至歷史資料庫。

1. **MTCNN （Multi-task Cascaded Convolutional Networks）**
    - 用於人臉檢測的深度學習模型，透過三層卷積神經網路（CNN）能夠有效地檢測和定位圖像中的人臉。
2. **DeepSORT** 
    - 用於深度學習的多目標追蹤演算法，結合利用深度學習得到的特徵提取和外觀模型，專為實現高效而準確的目標追蹤而設計。
3. **FaceNet** 
    - 用於深度學習的人臉辨識演算法，透過三層卷積神經網路（CNN）從人臉圖像中提取特徵來實現準確的人臉比對。
![Untitled 1](https://github.com/daisy00000/Pedestrian-flow-monitoring-Detections-in-Library-by-Using-Deep-Learning-Technology/assets/121708806/6d274750-9230-46d2-97d8-fe3a7e5d329a)

## 介面設計

在這個系統中，我們為運用深度學習於圖書館人流監控提供了一個使用者友好的介面。系統主要包含四個頁面，分別是主畫面、查詢頁面、統計頁面和設定頁面。這些頁面提供了豐富的功能，讓圖書館管理者能夠有效地監控人流、查詢資料、進行統計分析和進行相關設定。

這些頁面的設計旨在提供直觀和易用的界面，讓圖書館管理者可以輕鬆地使用系統的各項功能，確保圖書館的運營和安全。我們相信，這個系統將為圖書館管理者提供實用且高效的工具，幫助他們更好地監控人流並提供良好的學習環境。

### 主畫面

在主畫面中，我們提供了開啟即時人流偵測和閉館人流檢查的按鈕，這些功能可以讓管理者即時了解圖書館的人流狀況。同時，主畫面也顯示了即時的人數和時間，讓管理者能夠迅速掌握當前的狀態。

- **OPEN**：開啟即時人流偵測
    - 會即時顯示入口、出口畫面並偵測人臉
- **CLOSE**：閉館人流檢查
    - 閉館時檢查館內是否有尚未離館者
        - 無人：自動關閉系統
        - 有人：顯示尚未離館人數以及列出所有未離館者的詳細資料，可手動將資料刪除
- 即時顯示對應人數和時間
- 偵測到特殊人士會立即顯示名字、發送警訊並寄送Email通知管理人員
![Untitled 2](https://github.com/daisy00000/Pedestrian-flow-monitoring-Detections-in-Library-by-Using-Deep-Learning-Technology/assets/121708806/ccf2b6c5-4f34-447b-b8c1-403d055dd84f)

### 查詢頁面

在查詢頁面中，管理者可以根據特定條件進行查詢，包括時間段、ID、姓名、學號、員編和圖片。查詢結果將以表格的形式顯示在右側，方便管理者進行資料查閱。此外，管理者還可以透過勾選特殊名單的選項，只顯示特殊名單的資料，以便更快地查找相關信息。

- 可以使用時間段、ID、姓名、學號、員編、圖片進行查詢，查詢結果將顯示在右側的表格中。
- 右下方的框可以勾選，只顯示特殊名單在右側的表格中。
- 右下方的新增按鈕可以用來新增特殊名單，只需勾選所需的資料並填寫姓名、學號即可。
![Untitled 3](https://github.com/daisy00000/Pedestrian-flow-monitoring-Detections-in-Library-by-Using-Deep-Learning-Technology/assets/121708806/3a3edda3-dbf5-4678-a956-df63be35d15d)

### 統計頁面

在統計頁面中，管理者可以根據設定的起訖日期和圖表類型，繪製人數統計圖和人數趨勢分析圖。系統支援多種圖表類型，如長條圖和折線圖，以滿足不同的分析需求。同時，管理者還可以將統計結果匯出為CSV、EXCEL、圖片（.jpg）和PDF格式，方便進一步的數據分析和報告生成。

利用以下設定來繪製圖表

- 設定圖表的起訖日
- 設定圖表類型 (長條圖、折線圖)
- 設定時間單位:
    
    
    | 時間單位 | 起訖日時長 |
    | --- | --- |
    | 日 | 7天以內 |
    | 日、週 | 一個月以內 |
    | 週、月 | 一年以內 |
    | 一年以上 | 月、年 |
- 設定匯出圖表的格式
    - CSV、EXCEL、Image(.jpg)、PDF
![Untitled 4](https://github.com/daisy00000/Pedestrian-flow-monitoring-Detections-in-Library-by-Using-Deep-Learning-Technology/assets/121708806/ba2decc7-24c3-4b31-b10b-5c53a744ea87)

### 設定頁面

在設定頁面中，管理者可以管理特殊名單和通知名單。特殊名單用於記錄特殊人士的資料，包括姓名、學號/員編和正臉照片。通知名單則用於設定接收警訊通知的對象，包括姓名和電子郵件地址。管理者可以輕鬆地新增、修改和刪除特殊名單和通知名單中的資料，以便及時更新相關信息。

- 通知對象設定: 輸入姓名及電子郵件後即可新增至通知對象名單，會立即顯示於右上角的表格中。也可以透過勾選右上角表格的項目進行修改及刪除通知對象的資料。
- 特殊名單設定: 輸入三個必填項目(姓名、學號/員編、正臉照)即可新增至特殊名單，立即會顯示在右下角的表格中。也可以透過勾選右上角表格的項目進行修改及刪除特殊名單的資料。
![Untitled 5](https://github.com/daisy00000/Pedestrian-flow-monitoring-Detections-in-Library-by-Using-Deep-Learning-Technology/assets/121708806/07fb33b4-09c6-46d7-a020-9e077731a1a6)

## **使用的硬體設備**

硬體設備是系統運作不可或缺的基石，其性能直接關係到系統的運算效能與處理能力。本研究採用性能較高的硬體配置，以確保系統能夠順利執行各項任務。

- **處理器(CPU)**：11th Gen Intel(R) Core(TM) i7-1165G7
- **顯示卡(GPU)**：NVIDIA GeForce MX330
- **記憶體(RAM)**：16GB DDR4 3200Mhz
- **鏡頭(Webcam)**：羅技(Logitech) C270i HD

## 使用**軟體與工具**

在系統的軟體與工具方面的選擇是確保開發環境的穩定性和效能。程式碼編輯器選擇Visual Studio Code，系統運行環境採用Anaconda。作業系統(OS)選用Windows 11 家用版，在程式語言的選用上採用Python。這些軟體與工具的結合，為本系統的開發提供一個有效的工作環境。

- **MySQL：**版本 8.0
- **Python：** 版本 3.9
- **Nvidia 驅動程序**： 版本 11.7
- **作業系統(OS)：**Windows 11 家用版
- **Visual Studio Code**
- **Anaconda**

## 系統安裝說明

以下為在 Windows 系統中設置和執行專案的詳細步驟。請依循這些指引以確保順利完成專案的環境搭建和執行程式。

### 步驟 1： Github下載系統程式

在 Windows 系統中使用命令提示字元克隆系統程式

```python
git clone https://github.com/daisy00000/Pedestrian-flow-monitoring-Detections-in-Library-by-Using-Deep-Learning-Technology.git
```

### 步驟 2： 設置 OpenCV 影片處理庫環境變數

在 Windows 系統中使用命令提示字元執行以下命令以設置環境變數，這能幫助快速找到鏡頭影像配置（優先順序）

```python
setx OPENCV_VIDEOIO_PRIORITY_MSMF 0
```

### **步驟 3：創建和啟用 Conda 虛擬環境**

A. 需先安裝anaconda

anaconda相關建置與安裝請參考：

[用conda建立及管理python虛擬環境](https://medium.com/python4u/%E7%94%A8conda%E5%BB%BA%E7%AB%8B%E5%8F%8A%E7%AE%A1%E7%90%86python%E8%99%9B%E6%93%AC%E7%92%B0%E5%A2%83-b61fd2a76566)

B. 創建虛擬環境：

在程式所在的資料夾中開啟命令提示字元並輸入以下指令

```python
conda create --name myenv python=3.9
```

C. 啟用虛擬環境：

在命令提示字元並輸入以下指令

```python
activate myenv
```

### **步驟 4： 安裝 Nvidia CUDA Toolkit （如有使用GPU再執行）**

注意: 電腦本身須內建Nvidia

在命令提示字元使用 Conda 安裝 CUDA Toolkit，確保使用版本 11.7：

```python
conda install cuda -c nvidia==11.7
```

### **步驟 5： 安裝系統所需套件**

在命令提示字元使用以下指令安裝系統所需的 Python 套件：

```python
pip install -r requirements.txt
```

### **步驟 6： 更改資料庫參數**

在MySQL中建立新的資料庫並更改main.py中的指令(換成你所建置的資料庫密碼及名稱)

MySQL相關建置與安裝請參考：

[MySQL 學習筆記(二) — 一分鐘輕鬆瞭解如何在Windows上安裝MySQL](https://chwang12341.medium.com/mysql-%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E4%BA%8C-%E4%B8%80%E5%88%86%E9%90%98%E8%BC%95%E9%AC%86%E7%9E%AD%E8%A7%A3%E5%A6%82%E4%BD%95%E5%9C%A8windows%E4%B8%8A%E5%AE%89%E8%A3%9Dmysql-63cce07c6a6c)

```python
conn = mysql.connector.connect(
    host='127.0.0.1',
    user='root',
	  password='your_password',   
    database='your_database'  
)
```

### **步驟 7： 執行程式**

```python
python main.py
```

### 備註：測試帳號密碼(發送通知郵件)

以下為預設通知gmail帳號，可自行更改main.py中的設定

```python
帳號：mcutest000@gmail.com
應用程式密碼：aijd aolm jyfu ahmo
```
