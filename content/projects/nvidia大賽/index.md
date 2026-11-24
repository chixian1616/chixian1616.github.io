---
title: "NVIDIA Physical AI 技術挑戰賽 / SO-101 Robot Learning Hackathon (作品構想書)"
date: 2026-10-23
description: "結合多模態 VLA 具身智能與手眼視覺伺服之端子自主動態夾放系統：基於 NVIDIA Isaac Sim 數位孿生與 Sim-to-Real 技術"
tags: ["Physical AI", "Embodied AI", "Isaac Sim", "Sim-to-Real", "機械手臂", "邊緣運算"]
showTableOfContents: true
---


## 檔案下載
這個企劃書 也是由我親手打造 但這篇的話 老師介入比較多 因為當時文件太趕 快要到繳交期限了 所以老師直接介入幫我修改 
(老師50% 我 25% 組員 25%)

<div style="border: 1px solid #e2e8f0; border-radius: 8px; padding: 14px 18px; margin-bottom: 1.5rem; display: flex; align-items: center; justify-content: space-between; gap: 12px;">
  <div>
    <strong>專案簡報 / 技術文件下載</strong><br>
    <small>檔案格式：PDF ・ 建議離線閱讀競賽說明與系統架構細節</small>
  </div>
  <a href="CSU智視導引羅伯特ROBOTICS企劃書.pdf" download="萬潤2026_多樣化端子定位與機械手臂抓取整合系統.pdf" style="padding: 8px 14px; border-radius: 6px; background: #2563eb; color: #fff; text-decoration: none; white-space: nowrap;">
    立即下載
  </a>
</div>


### 專案概要
現在的工業配電盤、車用線束及控制箱組裝中，很多 O 型壓著端子插接作業高度依賴人工目視與手動對位，容易引發疲勞、漏插或接觸不良等瑕疵。傳統自動化則依賴震動送料盤與高精度剛性治具，缺乏換線彈性且成本高昂。

本專案針對**散亂、無序擺放的工業端子**，提出一套  **「結合多模態 VLA 具身智能與手眼視覺伺服」** 的高性價比自主動態夾放系統。利用 **NVIDIA Isaac Sim** 建立數位孿生環境進行強化學習與領域隨機化（Domain Randomization）訓練，結合實體 **SO-ARM101 六軸開源機械手臂**，突破傳統剛性治具限制，實現端到端的精密順應裝配。

---

### 系統核心架構：分層式具身決策 (Hierarchical Embodied AI)
端到端的大型 VLA 模型因算力負擔大，難以直接應用於高頻率動態伺服。本系統將任務拆解為**「全域粗定位」**與**「局部精細伺服」**解耦協同：

1. **Eye-to-Hand 俯視全域感知（YOLO11-OBB 粗定位）**
   - 正上方全景攝影機擷取散亂端子工作區。
   - 透過 **YOLO11-OBB** 旋轉框模型快速過濾無效背景，輸出端子類別、中心座標 ，極大化降低後續大模型的運算開銷。
2. **手眼轉換與粗移動**
   - 利用 **四點校正（單應性矩陣 Homography Matrix）** 將影像像素映射至物理工作平面座標，驅動手臂末端快速逼近工件上方。
3. **Eye-in-Hand 局部精細操作（多模態 VLA 決策）**
   - 手臂末端攝影機近距離鎖定感興趣區域（ROI）。
   - 輸入局部影像與指令至輕量化 **VLA** 模型，利用 **動作塊預測機制** 生成包含 6 軸相對位姿變化與夾爪開合狀態的軌跡序列，達成毫秒級平滑閉環伺服。
4. **Isaac Sim 數位孿生與 Sim-to-Real 虛實遷移**
   - 在 Isaac Sim 物理模擬環境中執行大規模平行強化學習（DRL）訓練手眼視覺伺服策略。
   - 導入**領域隨機化（Domain Randomization）**，模擬桌面摩擦力、光源反光與馬達延遲，使虛擬環境訓練出的策略模型能無縫遷移（Zero-Shot / Few-Shot）至真實世界。

---

### 技術規格與實作清單
* **硬體平台**：SO-ARM101 六軸開源機械手臂、客製化定位端子台、雙相機系統（Eye-in-Hand + Eye-to-Hand）。
* **邊緣運算晶片**：NVIDIA Jetson Thor（維持 30+ FPS 即時控制頻率與防碰撞路徑規劃）。
* **離線模擬與訓練**：NVIDIA Isaac Sim、Brev GPU 雲端訓練環境（DRL 視覺伺服策略約 2~4 小時收斂）。
* **軟體與演算法**：
  - YOLO11-OBB 定向邊界框偵測
  - 輕量化 Vision-Language-Action (VLA) 具身模型
  - 平面單應性矩陣（Homography Matrix）座標標定
  - TensorRT 模型量化加速、ROS 2、Python 3.10+ / PyTorch

---
