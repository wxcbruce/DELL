# Install Document

# Dell 產學合作安裝指南

## 前置需求
- 下載並安裝 FFmpeg ([安裝教學參考](https://vocus.cc/article/64701a2cfd897800014daed0))
- 設定 FFmpeg 環境變數
- 安裝 VSCode
- VSCode Python 擴充套件

## 安裝步驟

### 1. 取得專案檔案
```bash
git clone https://github.com/imlacha/tcpip_for_sts.git
```
或直接下載 ZIP 檔案

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

## UI討論
### 1. Host and client介面區別方式，利用帳號區分? 或是其他方式?
### 2. Host: 
● 選擇script的按鈕 Load script按鈕 Start按鈕 Assign/Reassign按鈕

● 顯示每一ROUND成功率以及轉譯後的文本
### 3. Client: 
● 統一更改Host Address

● 顯示被Assign的角色(發聲或收聲)、對話內容、時間戳以及回傳音檔完整過程

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

## 執行說明

1. 確保所有設備在同一網域下

2. 切換至正確目錄:
```bash
cd tcpiptest
```

3. 確認 Host IP:
```bash
ipconfig /all    # 查看 IPv4 位址
```

4. 啟動服務:
- Host 端:
```bash
python host-new.py
```
- Client 端:
```bash
python cli.py    # 記得修改連線位址為 host 端 IP
```

## 注意事項
- Host 端建議使用具有 GPU 的設備
- 確保所有設備都在同一網域下
- 執行前必須位於 tcpiptest 目錄內
