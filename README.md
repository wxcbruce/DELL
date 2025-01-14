# Install Document

# Dell 產學合作安裝指南

## 前置需求
- 下載並安裝 FFmpeg ([安裝教學參考](https://vocus.cc/article/64701a2cfd897800014daed0))
- 設定 FFmpeg 環境變數
- 安裝 VSCode
- VSCode Python 擴充套件
- 準備Openai的API Key: 首先註冊openai會員，進入 ([openai平台](https://platform.openai.com/chat-completions)) 後，找到左方API KEY選項，點選create new secret key，創建完成後請記得"一定要複製"，因為介面一關掉之後就沒辦法再複製API KEY了。接下來點選左方Usage會跳入下一畫面，再點選左方Billing，並點選Add a credit加值，如此便可使用openai付費服務。
- 在程式碼的keys.yaml中，貼上
```bash
api_keys : 上一步驟所複製下來的api key
```


## 安裝步驟

### 1. 取得專案檔案
```bash
git clone https://github.com/imlacha/tcpip_for_sts.git
```
or 直接下載 ZIP 檔案 or 隨身碟直接複製到dell本地 

### 2. 環境設定
根據機器角色選擇安裝對應的套件:
- Host 端:
```bash
pip install requirement-host.txt
```
包含以下套件:
faster-whisper, 
OpenCC, 
pandas, 
openpyxl

- Client 端:
```bash
pip install requirement-client.txt
```
包含以下套件:
ffmpeg-python, 
pydub, 
ffprobe, 
pyyaml, 
pyttsx3, 
PyAudio, 
noisereduce

## 執行前注意

1. 確保所有設備在同一網域下

2. 切換至正確目錄:
```bash
cd tcpiptest
```

3. 確認 Host IP:
```bash
ipconfig /all    # 查看 IPv4 位址
```
確認完IP位址後要將client端預連線位址更改為Host IP

## 使用說明

### 1. HOST端執行程式，開啟服務連線
```bash
python host.py
```
### 2. client端執行程式，連線至伺服器端
```bash
python client.py
```
### 3. 準備script檔，可以是excel或json格式(HOST端輸入)
```bash
load your_scriptfilename.xlsx
```
### 4. 依據script檔案的內容，將角色分配給client端(HOST端輸入)
```bash
assign
```
### 5. 各台client端拿到角色後即得知接下來要做什麼動作 ex.發聲或收音 故可開始執行 (HOST端輸入)
```bash
start
```
### 6. 如想關閉連線，可輸入以下(HOST端輸入)
```bash
stop
```

## 常見問題解決方案

### 1. libiomp5.dylib 初始化問題
在程式最上方加入以下代碼:
```python
import os
os.environ["KMP_DUPLICATE_LIB_OK"]="TRUE"
```

### 2. cublas64_11.dll 找不到
此問題發生於 host 端使用 fast-whisper 時:
1. 找到 Python 環境的 bin 資料夾
2. 確認是否有 cublas64_12.dll
3. 複製 cublas64_12.dll 並重新命名為 cublas64_11.dll


## 注意事項
- Host 端建議使用具有 GPU 的設備
- 確保所有設備都在同一網域下
- 執行前必須位於 tcpiptest 目錄內
