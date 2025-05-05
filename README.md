## 組員

林國善
41136111 資訊工程系3年級乙班

吳柏毅
41143262 資訊工程系3年級乙班

王馨卉
41146102 企業管理系3年級甲班

# 題目 牙醫診所掛號管理資料庫系統

---
## 應用情境

  在台灣，許多地區的牙醫診所病患的掛號紀錄可能因使用紙本容易遺失而無法追蹤，或者醫生無法快速查詢病患的歷史就診資料，進而影響診斷效率。

  為了改善這些問題，本系統旨在提供一個簡單可行、架構清晰的診所掛號資料庫管理系統，協助中小型診所有效管理病患資訊、醫療紀錄與掛號流程。
## 使用案例

  病患提供姓名、聯絡方式與希望的看診時間。
系統檢查醫師與診間的可用時段。
確認預約並記錄至資料庫，通知病患預約詳情。
## 專案簡介

### 功能
- **病患管理**：新增、查詢與更新病患資訊。
- **預約系統**：安排與檢視預約行程。
- **看診紀錄**：儲存病患看診的紀錄。

## 使用案例
### 病患預約

- 病患提供姓名、聯絡方式與希望的看診時間。
- 系統檢查醫師與診間的可用時段。
- 確認預約並記錄至資料庫，通知病患預約詳情。

### 管理者

- 管理者輸入醫師姓名與可用時段。
- 系統檢查是否有時間衝突並儲存排班資料。

## 系統需求說明

- 病患管理：記錄病患的基本資訊。
- 醫生管理：記錄醫生的基本資訊。
- 預約管理：支援新增、修改、查詢與取消預約，也提供預約時間衝突檢查功能。
- 就診管理：記錄病患的就診紀錄。

## 完整性限制

## patients 表（病患資料表）

![image](https://github.com/user-attachments/assets/7c8cd3eb-d4af-48c8-8c91-863dc541f686)

## doctors 表（醫生資料表）

![image](https://github.com/user-attachments/assets/4747824c-8089-4eed-be58-7a6f350d50b3)

## appointments表（預約資料表）

![image](https://github.com/user-attachments/assets/93fe0864-0899-4580-85a4-033120e594af)

## visits表（就診資料表）

![image](https://github.com/user-attachments/assets/96fc1c7b-20b2-4cc5-b4ec-82be0754a140)

---

## 資料庫建立流程

以下是建立 ClinicDB 資料庫的標準流程：

### 1. 需求分析
- **目標**：管理病患資料、預約與醫療紀錄。
- **範例需求**：
  - 病患：姓名、電話、生日、身份證字號。
  - 預約：時間、醫生。
  - 看診紀錄：病患、看診醫生、看診日期

### 2. 概念設計

## 一對多的關聯

![image](https://github.com/user-attachments/assets/54a8319e-b0f0-49c6-aca8-cf4a38415655)

![image](https://github.com/user-attachments/assets/763de2c5-cae5-4c2b-b8f1-165b5f138885)
## ER Diagram

![Image](https://github.com/user-attachments/assets/9984557d-b23c-47c0-a3f7-c778ead34ba4)


## 簡報
https://www.canva.com/design/DAGj82tfSmY/Q-CFpZqbAzo32BPzIDAeGA/edit
