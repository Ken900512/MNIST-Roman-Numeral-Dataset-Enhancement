# **RomanMNIST: 手寫羅馬數字辨識與數據增強**

## **專題介紹**
本專題著重在對於數據集進行改良，而非過往以改良模型為主的作法。首先利用Cleanvision來檢測與清理資料，然後透過錯誤標籤的修正、數據增強(生成更多元的圖片)來提升模型辨識的能力。最終，在模型不變的情況下將準確率從50%提升到80%左右。

---

## **資料集與改良方法**

### **資料來源**
- 原始資料集:  
  - 訓練集: 3367 張影像  
  - 驗證集: 963 張影像  
  - 測試集: 52 張影像  

- 資料特點:  
  - 格式: 灰階手寫羅馬數字(I~X)
  - 影像品質不均
  - 標籤分類有錯誤
  - 有部手寫數字難以辨識或非羅馬數字
  
---

## **改良方法**

### 1. **錯誤標籤修正**  
- 解決方法:
  1. 手動將錯誤分類的圖片放回正確的類別  
  2. 將不清楚或是非羅馬數字的圖片直接刪除  

- 此步驟將準確率提升至70%左右

### 2. **外部資料集**
- 目的與做法:
  1. 增加照片的多樣性，本次利用了Chars74k dataset，此資料集較多高清圖片
  2. 此步驟每個類別都增加了70-90張新影像

- 此步驟將準確率提升至75%左右

### 3. **影像清理**
利用CleanVision套件來進行處理  

- 部分資料問題 :  
  - 低資訊量（Low Information）
  - 過亮 / 過暗影像（Light/Dark）
  - 重複影像（Near Duplicates）
  
- 解決方法: 直接刪除有問題的影像

### 4. **影像增強**
- 目的: 增加數據量，能讓模型學習到各種狀態的照片

- 增強方式:
  - 訓練集 :
    - 隨機旋轉：±10%(36度）
    - 隨機縮放：±20%
    - 隨機平移：±15%
    - 隨機對比度：0.1~0.2
  
  - 驗證集 :
    - 旋轉範圍較小(±5%）
    - 縮放範圍較小(±10%)

- 此步驟將訓練集擴增至 10503 張，驗證集擴增至 3265 張

### 5. **最終處理**
- 使用Cleanvision再次清理增強完之後的數據
- 最終訓練集有9000張，驗證集有2940張
- 將準確度提升至80%左右

---

## **結語**
在本次研究中，影響到模型準確率最主要的原因是錯誤標籤，必須要優先處理，不然會讓模型學習到錯誤的部分。後續的資料清理以及資料擴充也成功讓模型的準確率上升，也顯示多元的資料確實能提升模型泛化的能力。未來或許能夠將錯誤標籤的處理透過自動化的方式進行，或者是增加更多元的外部資料集，將資料處理的部分更加完善。

---

## **工具**
- Python（pandas、numpy、matplotlib）  
- 機器學習（TensorFlow、Keras)
- 影像處理（CleanVision）
- 數據增強（TensorFlow Image Augmentation）

---

## **參考資料**
- [Kaggle Dataset - Handwritten Roman Digits](https://www.kaggle.com/datasets/agneev/basedonenglishhandwrittencharactersmodified)
- [CleanVision 影像清理工具](https://www.cnblogs.com/luohenyueji/p/18499084)
- [Chars74k Dataset](https://www.kaggle.com/datasets/agneev/basedonenglishhandwrittencharactersmodified)
- [Preparing a Roman MNIST Dataset](https://agneevmukherjee.github.io/agneev-blog/preparing-a-Roman-MNIST/)

---  

## **結構**
RomanMNIST    
│── README.md  
│── MNIST.pdf # 書面報告  
│── MNIST_code.ipynb # 程式碼  
│── MNIST_reprt.pdf  # 簡報  