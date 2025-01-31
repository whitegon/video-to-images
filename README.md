需求軟體
---
- Python 3
- opencv2
- labelImg

工具
將黃老師提供資料做標註
----------------
## 按照可見距離
- 小於30cm
- 30~40cm
- 40~50cm
- 大於50cm
- 未分類(?
------
## 再按照影像類型可分  
- 可見光(Visible)
  - 清澈水質
  - 綠色水（油綠、黃綠、履帶褐等）--優勢種類多為硅藻和隱藻
  -  褐色水（黃褐、紅褐、褐帶綠等）---優勢種類多為硅藻，同時有較多的微細浮游植物
  - 微霧
- 紅外線(Infrared，IR)

--------
## 綜合兩者可歸納
|          | 清澈           | 黃褐色   | 綠色            | 紅外線         |
|----------|----------------|----------|-----------------|----------------|
| 小於30cm |                |          |                 | 4部3GB         |
| 30~40cm  |                |          | 13部3GB         | 14部3GB        |
| 40~50cm  |                |          | 12部50MB10部3GB | 10部20MB7部3GB |
| 大於50cm | 77部(200M~1GB) | 3部300MB | 18部50MB        | 77部100MB      |
| 未分類   |                |          |                 |                |

## 標注工作狀況
## 如何標註資料
-------------------
#### 安裝 [labelImg](https://github.com/tzutalin/labelImg)
至官方的GitHub下載至電腦
#### 選擇要標註的影片
[Google drive 下載連結 需要要求權限](https://drive.google.com/drive/u/2/folders/17Q1iPxzFqPdqgBEmM-UsBOuUG3jNJzlz)
####
#### 大於50cm 
 - 黃褐色
    - 非常混濁 KAIYA_VIS_11cm20190502_151609.avi 的副本
    - 非常混濁 KAIYA_VIS_11cm20190502_143754.avi 的副本
    - 非常混濁 KAIYA_VIS_11cm20190502_143754.avi 的副本
 - 綠色(偏淺綠色)
    - 單純背景 有些許水草 2019-06-19-09_57_22.mp4
    - 有蝦子 無水草 2019-06-19-06_12_22.mp4
 - 清澈水質
    - 有蝦子 背景有大量飼料 4_10_R_180814132944.avi
 - 水質相對混濁(與清澈水質不太一樣)
    - 背景無飼料單純鐵網 2019-06-19-17_43_51.mp4
    - 背景無飼料但有蝦殼和沈澱物 2019-06-20-05_44_17.mp4
    - 背景有些許飼料 2019-06-20-10_14_17.mp4
    - 背景無飼料但有沈澱物 2019-06-20-17_47_07.mp4

### 執行 main.py 將影像轉成圖片
執行pip install 安裝opencv 及相關檔案
```console
$ pip3 install -r requirements.txt
```
 -i 為 輸入影像路徑 -r 要把圖片resize 成 r * r 影像 ，若不輸入則預設輸出原尺寸
```console
$ python3 main.py -i ./video.avi -r 256 
```
### 切換至 labelImag 路徑 並執行
IMAGE_PATH 為圖片路徑  
PRE-DEFINED CLASS FILE 為預先定義的label檔案 蝦子範例請見 classes.txt
```console
python3 labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```
### 開啟先選擇輸出label資料夾(與輸入資料夾分開)
![](./figs/labelImg3.png)
### 開啟後畫面
![](./figs/labelImg2.png)
### 點擊左下角將voc改成yolo
![](./figs/labelImg8.png)
![](./figs/labelImg1.png)
![](./figs/labelImg7.png)
### 開始標記（鍵盤 ｗ為標記 a為上一張 d 為下一張 ctrl+s 存擋）
![](./figs/labelImg4.png)
![](./figs/labelImg5.png)
![](./figs/labelImg6.png)
### 最後將 輸出label及原resize影像 分開壓縮成zip檔
resize影像資料夾 重新命名為 `wXh` w和h代表寬X高  
label資料夾則重新命名成`水質種類``張數`_`label`_`標記人英文名縮寫`
ex.   
若輸入資料夾 為尺寸256*256的照片 重新命名為`256X256`  
label資料夾 如果為標記黃褐色水質1000張 名字為 `brown1000_label_CK`

-------
#### DEMO 可用
 - 清澈
    - 13_10_R_180814150238.avi

