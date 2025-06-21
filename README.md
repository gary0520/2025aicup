# 2025 AICUP

本專案整合了 HuggingFace Whisper 模型、WhisperX 轉錄工具，以及 CTranslate2 模型加速格式轉換流程，建立一個完整的語音轉文字與文字實體抽取流程，主要應用於中文與英文醫療語音檔案的處理與標註。

## 專案結構與說明

### 1. `run answer1.ipynb` — 語音轉錄文本
主要流程包含：
- 使用whisper large-v3轉錄文本
- 輸出 `task1_answer.txt` 

### 2. `hf2ct-colab.ipynb` — HuggingFace 模型轉換與推論流程
此筆記本主要涵蓋：
- Whisper 模型的微調模型載入與架構建立
- 語音資料集處理與 `WhisperProcessor` 特徵抽取
- WhisperX 模型的應用：使用 WhisperX 進行語音轉錄與字詞對齊
- 模型轉換為 CTranslate2 格式，加速部署
- 最終將預測結果儲存為 JSON 與文字格式，支援後續標註與分析
使用的工具：
- `transformers`, `whisperx`, `ctranslate2`, `datasets`, `jiwer`, `torch`

---

### 3. `mistral.ipynb` — Mistral 模型應用與推論設定
此筆記本內容聚焦於：
- 微調 Mistral-7B-Instruct-v0.2 模型
- 載入 Mistral-7B-Instruct-v0.2模型並加載 LoRA 微調結果
- 以 JSON prompt 格式進行指定類型的個資（如 DOCTOR, DATE 等）抽取
- 對模型輸出進行格式檢查與結構化（JSON 解析）
- 將推論結果儲存至指定的檔案
- 針對不同PHI用不同函式做後處理
- 結合 WhisperX 對齊結果，為每個預測實體加上開始/結束時間戳
- 輸出 `task2_answer.txt` 

特點：
- 適用於中英文醫療語句中的實體抽取任務（SHI 任務）
- 針對資料格式一致性與結構穩定性設計了錯誤處理與修正邏輯

---
### 3. `GPT資料夾` — GPT4o直接抽取敏感字詞
- 輸出 不同類別的敏感字詞供資料後處理

特點：
- 使用沒有訓練過的GPT模型直接進行抽取敏感字詞的動作
---

## 運行環境

### 使用 Anaconda 建立環境

推薦使用 Anaconda 管理虛擬環境，指令如下：

```bash
conda env create -n lin python=3.11
conda activate lin
```

### 一、作業系統  
使用 **Linux (Ubuntu 20.04)** 作業系統。

### 二、硬體設置  
- **GPU**：使用 NVIDIA GeForce RTX 3090 Ti 顯示卡，擁有 24GB 顯存。

### 三、程式語言與套件  
- **Python 3.11**：主要編程語言，廣泛應用於深度學習領域。  
- **TensorFlow 2.8.0** 和 **PyTorch 1.9.0**：作為深度學習框架，用於構建和訓練神經網絡模型。  
- **NumPy 2.2.5**、**pandas 2.2.3**、**scikit-learn 1.6.1**：數據處理和機器學習所需的基礎庫。  
- **Librosa 0.11.0** 和 **PyTorch Audio 2.7.0**：用於音頻特徵提取與處理。  
- **CUDA 11.7** 和 **cuDNN 8.5**：支援 GPU 加速訓練。

### 四、預訓練模型與外部資源  
- **HuggingFace Transformers (4.50.0)**：提供多種預訓練語言模型。  
- **WhisperX (3.3.4)**：用於高效的語音辨識和語音轉文本任務。  
- **mistralai/Mistral-7B-Instruct-v0.2**：用此預訓練模型提取敏感資訊。

### 五、其它工具  
- **Wandb 0.20.1**：用於模型訓練過程中的實驗跟踪和可視化。

