ARIA v3.0: 降雨動態地圖與災害模擬分析系統
Week 5 Lab: Dynamic Mapping & Time-Machine Simulation

專案簡介
本專案為空間資訊系統課程之實驗成果。核心目標是建立一個能夠整合「即時氣象資料」與「歷史災害情境」的防災決策支援系統。透過 Python 串接氣象署 (CWA) API，並結合 GeoPandas 空間分析，評估避難所在極端降雨下的安全風險。

核心功能
即時 API 串接：自動獲取並解析中央氣象署 (CWA) 降雨觀測資料。

時光機模擬 (Simulation)：重現 2025 年「鳳凰颱風 (Typhoon Fung-wong)」蘇澳 130.5mm/hr 之極端降雨情境。

空間風險評估：利用 Buffer 分析 與 Spatial Join 自動篩選受威脅避難所。

互動式視覺化：產出包含熱度圖 (HeatMap) 與動態風險標記 (Exclamation Markers) 的 Folium 地圖。

目錄結構
Week5_Student.ipynb: 主要分析程式碼。

output/: 存放產出的互動式地圖 (.html)。

data/scenarios/: 鳳凰颱風歷史模擬資料 (.json)。

requirements.txt: 環境依賴清單。

.env.example: 環境變數設定範例。

實驗心得與問答 (Lab Questions)
1. 座標系統 (CRS) 的重要性
若忘記轉換 CRS，程式會因為單位不統一（度 vs 公尺）導致緩衝區範圍失控（例如 5 公里變成 5000 度），或觸發 ValueError。

2. CWA 為何使用 -998？
-998 是為了相容舊式軟體的數值格式。在現代分析中，必須將其轉換為 NaN 或 0 才能確保平均值等統計計算正確。

3. 優先撤離決策
在鳳凰颱風情境中，建議優先撤離受蘇澳 130.5mm 雨帶覆蓋且 Dynamic Risk = CRITICAL 的避難所。秉持「雨量決定威脅速度，地形決定致災強度」的原則。

4. 實驗挑戰與解決
最大的挑戰在於座標系統轉換與模擬場景的距離偏差（蘇澳至花蓮約 70km）。透過將影響半徑調整為 80 公里，成功驗證了空間風險連結的邏輯。
