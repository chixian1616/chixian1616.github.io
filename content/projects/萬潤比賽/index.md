---
title: "多樣化端子定位與機械手臂抓取整合系統｜萬潤 2026 創新創意競賽"
date: 2026-11-01
slug: "yolo11-obb-dobot-terminal-sorting-system"
description: "整合 YOLO11-OBB 旋轉框姿態估測、Homography 四點座標校正與 Dobot Magician 機械手臂，實現無固定治具下多樣化工業端子（I/O/Y型）自主定位、動態轉角夾取與智慧分選之機電整合系統。"
categories: ["專案作品", "競賽經歷"]
tags: ["電腦視覺", "YOLO11", "OBB定向邊界框", "機械手臂", "Homography座標校正", "智慧製造", "機電整合"]
image: "/images/posts/terminal-sorting-cover.png" # 建議放圖7實體工作站或圖1系統架構圖
showTableOfContents: true
draft: false
---
### 檔案下載
這是因為報名萬潤 2026 比賽而製作的企劃書，這份企劃書花了我蠻多時間的。因為第一次做比較正式的企劃書，當初做的時候連 Word 都還不太會用，所以也花了一點時間在研究 Word。老師也提供給我一些指導，像是第 13 頁的參考文獻怎麼找尋、格式怎麼設計。第一次做還是有點生疏，這份企劃書其實還有很多東西要改進，但因為時間的關係沒辦法改了……所以最終版是長這樣。
這份企劃書也可以讓你對我做的專題更了解在幹嘛。(這份企劃書的分工老師10% 我90% 組員0%)
<div style="border: 1px solid #e2e8f0; border-radius: 8px; padding: 14px 18px; margin-bottom: 1.5rem; display: flex; align-items: center; justify-content: space-between; gap: 12px;">
  <div>
    <strong>專案簡報 / 技術文件下載</strong><br>
    <small>檔案格式：PDF ・ 建議離線閱讀競賽說明與系統架構細節</small>
  </div>
  <a href="萬潤企劃書.pdf" download="萬潤2026_多樣化端子定位與機械手臂抓取整合系統.pdf" style="padding: 8px 14px; border-radius: 6px; background: #2563eb; color: #fff; text-decoration: none; white-space: nowrap;">
    立即下載
  </a>
</div>



### 專案概要
在傳統電子零組件製造產線中，端子與小型接頭的定位取放高度仰賴人工目檢或固定治具。人工長時間重複作業易因疲勞導致漏取與方向錯誤；而傳統固定治具缺乏彈性，一旦工件規格改變或散亂放置，就需要耗費高額成本重新開模與校正程式。

### 技術架構與負責項目
- **深度學習與視覺**：YOLO11 OBB、OpenCV、Python
- **座標轉換演算法**：透視變換（Homography 4-Point Calibration）、三角反切線姿態解算
- **邊緣部署**：本機離線推論與硬體通訊協議串接

### 成果動態展示

> 系統辨識 I/O/Y 型端子姿態後，自動換算角度並驅動機械手臂完成分選。

<video autoplay loop muted playsinline width="60%">
  <source src="dobotCIF.mp4" type="video/mp4">
</video>