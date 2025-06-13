## 組員

林國善
41136111 資訊工程系3年級乙班
製作github

吳柏毅
41143262 資訊工程系3年級乙班
實作資料庫、製作報告

王馨卉
41146102 企業管理系3年級甲班
製作報告

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

### 醫生

- 查看病患看診紀錄。
- 查看病患的預約詳情。
- 紀錄病患的就診紀錄。

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

![image](https://github.com/user-attachments/assets/cb0d9a71-174b-4554-902e-59dffaf37451)


## doctors 表（醫生資料表）

![image](https://github.com/user-attachments/assets/254dae16-2ce8-477f-817f-c840501a7fde)


## appointments表（預約資料表）

![image](https://github.com/user-attachments/assets/2eb1fe4b-bc24-4c07-9041-fbfd989b5164)


## medical_record表（病歷資料表）

![image](https://github.com/user-attachments/assets/defb29a2-6243-4143-abbf-a02e0c356073)


## schedule表（排班資料表）

![image](https://github.com/user-attachments/assets/70fd30d2-b67d-460e-abde-0dbb2d881f7a)

## user 表（使用者帳號密碼資料表）

![image](https://github.com/user-attachments/assets/b29c0b8c-d604-4f32-a952-43ec69da200a)

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

實體與關連的摘要圖

![Image](https://github.com/user-attachments/assets/5a31f220-78db-40a2-b906-dfe7f39c10f0)

詳細全圖

![Image](https://github.com/user-attachments/assets/5f6c9771-6a37-456a-9c35-00bc002d9e2b)

用戶

![image](https://github.com/user-attachments/assets/391ea252-c1fd-4547-93ed-7d971e288a66)

病患

![image](https://github.com/user-attachments/assets/4baba63a-e3a9-4f3b-af28-835635ff39b1)

醫生

![image](https://github.com/user-attachments/assets/076cde50-76d0-4d3d-a41a-3de538878d80)

預約

![image](https://github.com/user-attachments/assets/ac2908fd-5c45-49bd-9ccd-e84e08e28a6d)


## 病患資料表
```
CREATE TABLE patient (
    patient_id VARCHAR(30) PRIMARY KEY,
    national_id TEXT NOT NULL,
    name TEXT NOT NULL,
    gender TEXT CHECK(gender IN ('男', '女')),
    birth_date DATE,
    phone TEXT
);
```

## 醫生資料表
```
CREATE TABLE doctor (
    doctor_id VARCHAR(30) PRIMARY KEY,
    name TEXT NOT NULL,
    specialty TEXT NOT NULL,
    phone TEXT
);
```

## 病歷表
```
CREATE OR REPLACE TABLE medical_record (
    medical_record_id VARCHAR(30) PRIMARY KEY,
    patient_id VARCHAR(30),
    diagnosis_record TEXT,
    visits_date DATE,
    FOREIGN KEY (patient_id) REFERENCES patient(patient_id)
);
```

## 預約表
```
CREATE OR REPLACE TABLE appointment (
    appointment_id VARCHAR(30) PRIMARY KEY,
    patient_id VARCHAR(30),
    schedule_id INTEGER,
    number VARCHAR(10),
    status TEXT,
    medical_record_id VARCHAR(30),
    FOREIGN KEY (patient_id) REFERENCES patient(patient_id),
    FOREIGN KEY (schedule_id) REFERENCES schedule(schedule_id),
    FOREIGN KEY (medical_record_id) REFERENCES medical_record(medical_record_id)
);
```

## 醫生排班表
```
CREATE OR REPLACE TABLE schedule (
    schedule_id INTEGER PRIMARY KEY,
    doctor_id VARCHAR(30),
    schedule_date DATE,
    schedule_time TEXT,
    week TEXT,
    clinic TEXT,
    schedule_status TEXT,
    FOREIGN KEY (doctor_id) REFERENCES doctor(doctor_id)
);

```

## 新增病患資料
```

INSERT INTO patient (patient_id, national_id, name, gender, birth_date, phone) VALUES
('P-2024-01', 'A225190428', '陳玉華', '女', '1970-10-24', '0912100200'),
('P-2024-02', 'B109235501', '黃志明', '男', '1985-12-25', '0922200300'),
('P-2024-03', 'C274705806', '林淑芬', '女', '1986-02-22', '0933300400'),
('P-2024-04', 'D117815766', '張文龍', '男', '1975-04-11', '0944400500'),
('P-2024-05', 'E253941742', '李玉美', '女', '1955-07-14', '0955500600'),
('P-2024-06', 'F110994720', '王志誠', '男', '1995-11-14', '0966600700'),
('P-2024-07', 'G231160530', '吳佩珊', '女', '2018-07-21', '0977700800'),
('P-2024-08', 'H131347152', '趙信宏', '男', '1983-08-24', '0988800900'),
('P-2024-09', 'I148658852', '劉文昌', '男', '1988-12-09', '0999900000'),
('P-2024-10', 'J260542851', '葉秋萍', '女', '1985-10-08', '0900111222'),
('P-2024-11', 'J102662605', '田可名', '男', '1975-10-21', '0911100777'),
('P-2024-12', 'E269884203', '孫泳宜', '女', '2000-09-21', '0919800732'),
('P-2024-13', 'F165045923', '柯峻鋒', '男', '1999-09-28', '0939002124'),
('P-2024-14', 'H147258175', '蘇耀元', '男', '1980-03-22', '0917783213'),
('P-2024-15', 'C205110417', '簡以心', '女', '1995-10-10', '0909842134');

```

## 新增醫生資料
```

INSERT INTO doctor (doctor_id, name, specialty, phone) VALUES
('D-001', '王大明', '牙科', '0932716195'),
('D-002', '李小美', '牙科', '0910775159'),
('D-003', '陳志強', '牙科', '0984593191'),
('D-004', '林慧君', '牙科', '0968202494'),
('D-005', '張建宏', '牙科', '0911858069'),
('D-006', '吳佩琪', '牙科', '0961519171'),
('D-007', '周俊豪', '牙科', '0977834772'),
('D-008', '鄭雅芳', '牙科', '0970379877'),
('D-009', '何文豪', '牙科', '0980671879'),
('D-010', '劉曉婷', '牙科', '0968500959');
```

## 新增病歷資料
```
INSERT INTO medical_record (medical_record_id, patient_id, diagnosis_record, visits_date) VALUES
('MR-001', 'P-2024-01', '蛀牙', '2024-08-07'),
('MR-002', 'P-2024-02', '牙周病', '2024-04-21'),
('MR-003', 'P-2024-03', '智齒拔除', '2024-09-04'),
('MR-004', 'P-2024-04', '牙齒美白', '2024-03-27'),
('MR-005', 'P-2024-05', '洗牙', '2023-11-19'),
('MR-006', 'P-2024-06', '牙齒矯正', '2024-02-14'),
('MR-007', 'P-2024-07', '補牙', '2024-03-13'),
('MR-008', 'P-2024-08', '牙齦炎', '2023-09-17'),
('MR-009', 'P-2024-09', '牙齒裂痕', '2024-07-15'),
('MR-010', 'P-2024-10', '牙冠製作', '2023-01-13'),
('MR-011', 'P-2024-11','洗牙', '1975-10-21'),
('MR-012', 'P-2024-12', '牙齒矯正', '2000-09-21'),
('MR-013', 'P-2024-13', '智齒拔除', '1999-09-28'),
('MR-014', 'P-2024-14', '牙齦炎', '1980-03-22'),
('MR-015', 'P-2024-15', '洗牙', '1995-10-10');

```

## 新增醫生排班資料

```
INSERT INTO schedule (schedule_id, doctor_id, schedule_date, schedule_time, week, clinic, schedule_status) VALUES
(1, 'D-001', '2025-05-21', '上午', '星期一', '101診間', '已滿'),
(2, 'D-002', '2025-05-22', '上午', '星期二', '101診間', '開診'),
(3, 'D-003', '2025-05-23', '上午', '星期三', '101診間', '開診'),
(4, 'D-004', '2025-05-24', '下午', '星期四', '102診間', '休診'),
(5, 'D-005', '2025-05-25', '下午', '星期五', '102診間', '開診'),
(6, 'D-006', '2025-05-26', '下午', '星期一', '103診間', '開診'),
(7, 'D-007', '2025-05-27', '下午', '星期二', '103診間', '開診'),
(8, 'D-008', '2025-05-28', '晚上', '星期三', '103診間', '休診'),
(9, 'D-009', '2025-05-29', '晚上', '星期四', '104診間', '開診'),
(10, 'D-010', '2025-05-30', '晚上', '星期五', '104診間', '開診');

```

## 新增預約表資料
```

INSERT INTO appointment (appointment_id, patient_id, schedule_id, number, status, medical_record_id) VALUES
('2025-04-21-001', 'P-2024-01', 1, '1號', '已完成', 'MR-001'),
('2025-04-22-002', 'P-2024-02', 2, '1號', '已預約', 'MR-002'),
('2025-04-23-003', 'P-2024-03', 3, NULL, '取消', 'MR-003'),
('2025-04-24-004', 'P-2024-04', 10, '1號', '已完成', 'MR-004'),
('2025-04-25-005', 'P-2024-05', 5, '1號', '已預約', 'MR-005'),
('2025-04-26-006', 'P-2024-06', 6, '1號', '已完成', 'MR-006'),
('2025-04-27-007', 'P-2024-07', 7, '1號', '已預約', 'MR-007'),
('2025-04-28-008', 'P-2024-08', 10, '1號', '已完成', 'MR-008'),
('2025-04-29-009', 'P-2024-09', 9, '1號', '已預約', 'MR-009'),
('2025-04-30-010', 'P-2024-10', 1, '2號', '已完成', 'MR-010'),
('2025-05-01-011', 'P-2024-11', 1, '3號', '已預約', 'MR-011'),
('2025-05-02-012', 'P-2024-12', 1, '4號', '已預約', 'MR-012'),
('2025-05-03-013', 'P-2024-13', 4, NULL, '取消', 'MR-013'),
('2025-05-04-014', 'P-2024-14', 2, '2號', '已預約', 'MR-014'),
('2025-05-05-015', 'P-2024-15', 1, '5號', '已預約', 'MR-015');

```


## 病人看到自己的預約結果(ID:P-2024-01)
```
CREATE OR REPLACE VIEW patient_view_01 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    d.name AS 醫生名字,
    d.specialty AS 科別,
    a.status AS 預約狀態,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時段,
    s.clinic AS 診間號碼,
    a.number AS 看診號碼,
    (
        SELECT COUNT(*)
        FROM appointment a2
        JOIN schedule s2 ON a2.schedule_id = s2.schedule_id
        WHERE a2.status = '已完成'
          AND s2.doctor_id = d.doctor_id
          AND s2.schedule_date = s.schedule_date
          AND s2.schedule_time = s.schedule_time
          AND s2.clinic = s.clinic
    ) + 1 AS 目前看診號碼
FROM patient p
LEFT JOIN appointment a ON p.patient_id = a.patient_id
LEFT JOIN schedule s ON a.schedule_id = s.schedule_id
LEFT JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE p.patient_id = 'P-2024-01';
```

## 病人看到自己的預約結果(ID:P-2024-02)
```
CREATE OR REPLACE VIEW patient_view_02 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    d.name AS 醫生名字,
    d.specialty AS 科別,
    a.status AS 預約狀態,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時段,
    s.clinic AS 診間號碼,
    a.number AS 看診號碼,
    (
        SELECT COUNT(*)
        FROM appointment a2
        JOIN schedule s2 ON a2.schedule_id = s2.schedule_id
        WHERE a2.status = '已完成'
          AND s2.doctor_id = d.doctor_id
          AND s2.schedule_date = s.schedule_date
          AND s2.schedule_time = s.schedule_time
          AND s2.clinic = s.clinic
    ) + 1 AS 目前看診號碼
FROM patient p
LEFT JOIN appointment a ON p.patient_id = a.patient_id
LEFT JOIN schedule s ON a.schedule_id = s.schedule_id
LEFT JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE p.patient_id = 'P-2024-02';
```
## 病人看到自己的預約結果(ID:P-2024-03)
```
CREATE OR REPLACE VIEW patient_view_03 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    d.name AS 醫生名字,
    d.specialty AS 科別,
    a.status AS 預約狀態,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時段,
    s.clinic AS 診間號碼,
    a.number AS 看診號碼,
    (
        SELECT COUNT(*)
        FROM appointment a2
        JOIN schedule s2 ON a2.schedule_id = s2.schedule_id
        WHERE a2.status = '已完成'
          AND s2.doctor_id = d.doctor_id
          AND s2.schedule_date = s.schedule_date
          AND s2.schedule_time = s.schedule_time
          AND s2.clinic = s.clinic
    ) + 1 AS 目前看診號碼
FROM patient p
LEFT JOIN appointment a ON p.patient_id = a.patient_id
LEFT JOIN schedule s ON a.schedule_id = s.schedule_id
LEFT JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE p.patient_id = 'P-2024-03';
```
## 病人看到自己的預約結果(ID:P-2024-04)
```
CREATE OR REPLACE VIEW patient_view_04 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    d.name AS 醫生名字,
    d.specialty AS 科別,
    a.status AS 預約狀態,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時段,
    s.clinic AS 診間號碼,
    a.number AS 看診號碼,
    (
        SELECT COUNT(*)
        FROM appointment a2
        JOIN schedule s2 ON a2.schedule_id = s2.schedule_id
        WHERE a2.status = '已完成'
          AND s2.doctor_id = d.doctor_id
          AND s2.schedule_date = s.schedule_date
          AND s2.schedule_time = s.schedule_time
          AND s2.clinic = s.clinic
    ) + 1 AS 目前看診號碼
FROM patient p
LEFT JOIN appointment a ON p.patient_id = a.patient_id
LEFT JOIN schedule s ON a.schedule_id = s.schedule_id
LEFT JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE p.patient_id = 'P-2024-04';
```
## 病人看到自己的預約結果(ID:P-2024-05)
```
CREATE OR REPLACE VIEW patient_view_05 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    d.name AS 醫生名字,
    d.specialty AS 科別,
    a.status AS 預約狀態,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時段,
    s.clinic AS 診間號碼,
    a.number AS 看診號碼,
    (
        SELECT COUNT(*)
        FROM appointment a2
        JOIN schedule s2 ON a2.schedule_id = s2.schedule_id
        WHERE a2.status = '已完成'
          AND s2.doctor_id = d.doctor_id
          AND s2.schedule_date = s.schedule_date
          AND s2.schedule_time = s.schedule_time
          AND s2.clinic = s.clinic
    ) + 1 AS 目前看診號碼
FROM patient p
LEFT JOIN appointment a ON p.patient_id = a.patient_id
LEFT JOIN schedule s ON a.schedule_id = s.schedule_id
LEFT JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE p.patient_id = 'P-2024-05';
```
## 病人看到自己的預約結果(ID:P-2024-06)
```
CREATE OR REPLACE VIEW patient_view_06 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    d.name AS 醫生名字,
    d.specialty AS 科別,
    a.status AS 預約狀態,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時段,
    s.clinic AS 診間號碼,
    a.number AS 看診號碼,
    (
        SELECT COUNT(*)
        FROM appointment a2
        JOIN schedule s2 ON a2.schedule_id = s2.schedule_id
        WHERE a2.status = '已完成'
          AND s2.doctor_id = d.doctor_id
          AND s2.schedule_date = s.schedule_date
          AND s2.schedule_time = s.schedule_time
          AND s2.clinic = s.clinic
    ) + 1 AS 目前看診號碼
FROM patient p
LEFT JOIN appointment a ON p.patient_id = a.patient_id
LEFT JOIN schedule s ON a.schedule_id = s.schedule_id
LEFT JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE p.patient_id = 'P-2024-06';
```
## 病人看到自己的預約結果(ID:P-2024-07)
```
CREATE OR REPLACE VIEW patient_view_07 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    d.name AS 醫生名字,
    d.specialty AS 科別,
    a.status AS 預約狀態,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時段,
    s.clinic AS 診間號碼,
    a.number AS 看診號碼,
    (
        SELECT COUNT(*)
        FROM appointment a2
        JOIN schedule s2 ON a2.schedule_id = s2.schedule_id
        WHERE a2.status = '已完成'
          AND s2.doctor_id = d.doctor_id
          AND s2.schedule_date = s.schedule_date
          AND s2.schedule_time = s.schedule_time
          AND s2.clinic = s.clinic
    ) + 1 AS 目前看診號碼
FROM patient p
LEFT JOIN appointment a ON p.patient_id = a.patient_id
LEFT JOIN schedule s ON a.schedule_id = s.schedule_id
LEFT JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE p.patient_id = 'P-2024-07';
```
## 病人看到自己的預約結果(ID:P-2024-08)
```
CREATE OR REPLACE  VIEW patient_view_08 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    d.name AS 醫生名字,
    d.specialty AS 科別,
    a.status AS 預約狀態,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時段,
    s.clinic AS 診間號碼,
    a.number AS 看診號碼,
    (
        SELECT COUNT(*)
        FROM appointment a2
        JOIN schedule s2 ON a2.schedule_id = s2.schedule_id
        WHERE a2.status = '已完成'
          AND s2.doctor_id = d.doctor_id
          AND s2.schedule_date = s.schedule_date
          AND s2.schedule_time = s.schedule_time
          AND s2.clinic = s.clinic
    ) + 1 AS 目前看診號碼
FROM patient p
LEFT JOIN appointment a ON p.patient_id = a.patient_id
LEFT JOIN schedule s ON a.schedule_id = s.schedule_id
LEFT JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE p.patient_id = 'P-2024-08';
```
## 病人看到自己的預約結果(ID:P-2024-09)
```
CREATE OR REPLACE VIEW patient_view_09 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    d.name AS 醫生名字,
    d.specialty AS 科別,
    a.status AS 預約狀態,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時段,
    s.clinic AS 診間號碼,
    a.number AS 看診號碼,
    (
        SELECT COUNT(*)
        FROM appointment a2
        JOIN schedule s2 ON a2.schedule_id = s2.schedule_id
        WHERE a2.status = '已完成'
          AND s2.doctor_id = d.doctor_id
          AND s2.schedule_date = s.schedule_date
          AND s2.schedule_time = s.schedule_time
          AND s2.clinic = s.clinic
    ) + 1 AS 目前看診號碼
FROM patient p
LEFT JOIN appointment a ON p.patient_id = a.patient_id
LEFT JOIN schedule s ON a.schedule_id = s.schedule_id
LEFT JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE p.patient_id = 'P-2024-09';
```
## 病人看到自己的預約結果(ID:P-2024-10)
```
CREATE OR REPLACE VIEW patient_view_10 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    d.name AS 醫生名字,
    d.specialty AS 科別,
    a.status AS 預約狀態,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時段,
    s.clinic AS 診間號碼,
    a.number AS 看診號碼,
    (
        SELECT COUNT(*)
        FROM appointment a2
        JOIN schedule s2 ON a2.schedule_id = s2.schedule_id
        WHERE a2.status = '已完成'
          AND s2.doctor_id = d.doctor_id
          AND s2.schedule_date = s.schedule_date
          AND s2.schedule_time = s.schedule_time
          AND s2.clinic = s.clinic
    ) + 1 AS 目前看診號碼
FROM patient p
LEFT JOIN appointment a ON p.patient_id = a.patient_id
LEFT JOIN schedule s ON a.schedule_id = s.schedule_id
LEFT JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE p.patient_id = 'P-2024-10';
```
## 病人看到自己的預約結果(ID:P-2024-11)
```
CREATE OR REPLACE VIEW patient_view_11 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    d.name AS 醫生名字,
    d.specialty AS 科別,
    a.status AS 預約狀態,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時段,
    s.clinic AS 診間號碼,
    a.number AS 看診號碼,
    (
        SELECT COUNT(*)
        FROM appointment a2
        JOIN schedule s2 ON a2.schedule_id = s2.schedule_id
        WHERE a2.status = '已完成'
          AND s2.doctor_id = d.doctor_id
          AND s2.schedule_date = s.schedule_date
          AND s2.schedule_time = s.schedule_time
          AND s2.clinic = s.clinic
    ) + 1 AS 目前看診號碼
FROM patient p
LEFT JOIN appointment a ON p.patient_id = a.patient_id
LEFT JOIN schedule s ON a.schedule_id = s.schedule_id
LEFT JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE p.patient_id = 'P-2024-11';
```
## 病人看到自己的預約結果(ID:P-2024-12)
```
CREATE OR REPLACE VIEW patient_view_12 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    d.name AS 醫生名字,
    d.specialty AS 科別,
    a.status AS 預約狀態,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時段,
    s.clinic AS 診間號碼,
    a.number AS 看診號碼,
    (
        SELECT COUNT(*)
        FROM appointment a2
        JOIN schedule s2 ON a2.schedule_id = s2.schedule_id
        WHERE a2.status = '已完成'
          AND s2.doctor_id = d.doctor_id
          AND s2.schedule_date = s.schedule_date
          AND s2.schedule_time = s.schedule_time
          AND s2.clinic = s.clinic
    ) + 1 AS 目前看診號碼
FROM patient p
LEFT JOIN appointment a ON p.patient_id = a.patient_id
LEFT JOIN schedule s ON a.schedule_id = s.schedule_id
LEFT JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE p.patient_id = 'P-2024-12';
```
## 病人看到自己的預約結果(ID:P-2024-13)
```
CREATE OR REPLACE VIEW patient_view_13 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    d.name AS 醫生名字,
    d.specialty AS 科別,
    a.status AS 預約狀態,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時段,
    s.clinic AS 診間號碼,
    a.number AS 看診號碼,
    (
        SELECT COUNT(*)
        FROM appointment a2
        JOIN schedule s2 ON a2.schedule_id = s2.schedule_id
        WHERE a2.status = '已完成'
          AND s2.doctor_id = d.doctor_id
          AND s2.schedule_date = s.schedule_date
          AND s2.schedule_time = s.schedule_time
          AND s2.clinic = s.clinic
    ) + 1 AS 目前看診號碼
FROM patient p
LEFT JOIN appointment a ON p.patient_id = a.patient_id
LEFT JOIN schedule s ON a.schedule_id = s.schedule_id
LEFT JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE p.patient_id = 'P-2024-13';
```
## 病人看到自己的預約結果(ID:P-2024-14)
```
CREATE OR REPLACE VIEW patient_view_14 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    d.name AS 醫生名字,
    d.specialty AS 科別,
    a.status AS 預約狀態,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時段,
    s.clinic AS 診間號碼,
    a.number AS 看診號碼,
    (
        SELECT COUNT(*)
        FROM appointment a2
        JOIN schedule s2 ON a2.schedule_id = s2.schedule_id
        WHERE a2.status = '已完成'
          AND s2.doctor_id = d.doctor_id
          AND s2.schedule_date = s.schedule_date
          AND s2.schedule_time = s.schedule_time
          AND s2.clinic = s.clinic
    ) + 1 AS 目前看診號碼
FROM patient p
LEFT JOIN appointment a ON p.patient_id = a.patient_id
LEFT JOIN schedule s ON a.schedule_id = s.schedule_id
LEFT JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE p.patient_id = 'P-2024-14';
```
## 病人看到自己的預約結果(ID:P-2024-15)
```
CREATE OR REPLACE VIEW patient_view_15 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    d.name AS 醫生名字,
    d.specialty AS 科別,
    a.status AS 預約狀態,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時段,
    s.clinic AS 診間號碼,
    a.number AS 看診號碼,
    (
        SELECT COUNT(*)
        FROM appointment a2
        JOIN schedule s2 ON a2.schedule_id = s2.schedule_id
        WHERE a2.status = '已完成'
          AND s2.doctor_id = d.doctor_id
          AND s2.schedule_date = s.schedule_date
          AND s2.schedule_time = s.schedule_time
          AND s2.clinic = s.clinic
    ) + 1 AS 目前看診號碼
FROM patient p
LEFT JOIN appointment a ON p.patient_id = a.patient_id
LEFT JOIN schedule s ON a.schedule_id = s.schedule_id
LEFT JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE p.patient_id = 'P-2024-15';
```
## 創建使用者
```
CREATE USER 'patient_P_2024_01'@'localhost' IDENTIFIED BY 'secure_password_01';
CREATE USER 'patient_P_2024_02'@'localhost' IDENTIFIED BY 'secure_password_02';
CREATE USER 'patient_P_2024_03'@'localhost' IDENTIFIED BY 'secure_password_03';
CREATE USER 'patient_P_2024_04'@'localhost' IDENTIFIED BY 'secure_password_04';
CREATE USER 'patient_P_2024_05'@'localhost' IDENTIFIED BY 'secure_password_05';
CREATE USER 'patient_P_2024_06'@'localhost' IDENTIFIED BY 'secure_password_06';
CREATE USER 'patient_P_2024_07'@'localhost' IDENTIFIED BY 'secure_password_07';
CREATE USER 'patient_P_2024_08'@'localhost' IDENTIFIED BY 'secure_password_08';
CREATE USER 'patient_P_2024_09'@'localhost' IDENTIFIED BY 'secure_password_09';
CREATE USER 'patient_P_2024_10'@'localhost' IDENTIFIED BY 'secure_password_10';
CREATE USER 'patient_P_2024_11'@'localhost' IDENTIFIED BY 'secure_password_11';
CREATE USER 'patient_P_2024_12'@'localhost' IDENTIFIED BY 'secure_password_12';
CREATE USER 'patient_P_2024_13'@'localhost' IDENTIFIED BY 'secure_password_13';
CREATE USER 'patient_P_2024_14'@'localhost' IDENTIFIED BY 'secure_password_14';
CREATE USER 'patient_P_2024_15'@'localhost' IDENTIFIED BY 'secure_password_15';
```

## 設定patient_view權限
```
GRANT SELECT ON hos.patient_view_01 TO 'patient_P_2024_01'@'localhost';
GRANT SELECT ON hos.patient_view_02 TO 'patient_P_2024_02'@'localhost';
GRANT SELECT ON hos.patient_view_03 TO 'patient_P_2024_03'@'localhost';
GRANT SELECT ON hos.patient_view_04 TO 'patient_P_2024_04'@'localhost';
GRANT SELECT ON hos.patient_view_05 TO 'patient_P_2024_05'@'localhost';
GRANT SELECT ON hos.patient_view_06 TO 'patient_P_2024_06'@'localhost';
GRANT SELECT ON hos.patient_view_07 TO 'patient_P_2024_07'@'localhost';
GRANT SELECT ON hos.patient_view_08 TO 'patient_P_2024_08'@'localhost';
GRANT SELECT ON hos.patient_view_09 TO 'patient_P_2024_09'@'localhost';
GRANT SELECT ON hos.patient_view_10 TO 'patient_P_2024_10'@'localhost';
GRANT SELECT ON hos.patient_view_11 TO 'patient_P_2024_11'@'localhost';
GRANT SELECT ON hos.patient_view_12 TO 'patient_P_2024_12'@'localhost';
GRANT SELECT ON hos.patient_view_13 TO 'patient_P_2024_13'@'localhost';
GRANT SELECT ON hos.patient_view_14 TO 'patient_P_2024_14'@'localhost';
GRANT SELECT ON hos.patient_view_15 TO 'patient_P_2024_15'@'localhost';
```
## 查看權限設定是否正確
```
SHOW GRANTS FOR 'patient_P_2024_01'@'localhost';
```
<img width="685" alt="image" src="https://github.com/user-attachments/assets/8d5d608b-a22d-4a2f-a186-df15dfa3213b" />

```
SHOW GRANTS FOR 'patient_P_2024_02'@'localhost';
```
<img width="688" alt="image" src="https://github.com/user-attachments/assets/ea943304-01f9-4692-b48e-adda51d092d3" />

```
SHOW GRANTS FOR 'patient_P_2024_03'@'localhost';
```
<img width="692" alt="image" src="https://github.com/user-attachments/assets/d129818a-e7a7-4c79-9037-186fc83eb532" />

```
SHOW GRANTS FOR 'patient_P_2024_04'@'localhost';
```
<img width="689" alt="image" src="https://github.com/user-attachments/assets/3bf6f8eb-53d5-4201-aec5-d5dd8a42cf21" />

```
SHOW GRANTS FOR 'patient_P_2024_05'@'localhost';
```
<img width="688" alt="image" src="https://github.com/user-attachments/assets/0ba057e2-a681-4d3a-b0c8-f335194d2d02" />

```
SHOW GRANTS FOR 'patient_P_2024_06'@'localhost';
```
<img width="686" alt="image" src="https://github.com/user-attachments/assets/a40dac90-c321-46d7-83fc-b6a2d4990c0b" />


```
SHOW GRANTS FOR 'patient_P_2024_07'@'localhost';
```
<img width="690" alt="image" src="https://github.com/user-attachments/assets/6e5c4f32-bdbc-44b3-85c2-e318558576ed" />


```
SHOW GRANTS FOR 'patient_P_2024_08'@'localhost';
```
<img width="691" alt="image" src="https://github.com/user-attachments/assets/76106882-2032-4837-8179-042c8fab691b" />


```
SHOW GRANTS FOR 'patient_P_2024_09'@'localhost';
```
<img width="684" alt="image" src="https://github.com/user-attachments/assets/a68bb436-4701-4317-98b0-3889bf8051e9" />


```
SHOW GRANTS FOR 'patient_P_2024_10'@'localhost';
```
<img width="689" alt="image" src="https://github.com/user-attachments/assets/83a5c458-c9fa-4305-b74f-e5e8f8182f80" />


```
SHOW GRANTS FOR 'patient_P_2024_11'@'localhost';
```
<img width="694" alt="image" src="https://github.com/user-attachments/assets/bdee53cf-1d1f-4204-af8b-f5db27b58f5e" />


```
SHOW GRANTS FOR 'patient_P_2024_12'@'localhost';
```
<img width="686" alt="image" src="https://github.com/user-attachments/assets/b537d173-a79c-4ee3-88f0-bf5a372fa708" />


```
SHOW GRANTS FOR 'patient_P_2024_13'@'localhost';
```
<img width="695" alt="image" src="https://github.com/user-attachments/assets/84c6d19e-f476-4600-8539-f7e88a654de4" />


```
SHOW GRANTS FOR 'patient_P_2024_14'@'localhost';
```
<img width="697" alt="image" src="https://github.com/user-attachments/assets/c27c4fba-f6b4-4350-9ca4-8746dcf52a4a" />

```
SHOW GRANTS FOR 'patient_P_2024_15'@'localhost';
```
<img width="689" alt="image" src="https://github.com/user-attachments/assets/3c11f79c-d65f-4cbd-b7c9-b0aac98861d1" />







## 使用ID:P-2024-01登入
```
mysql -u patient_P_2024_01 -p -h localhost
```
## 查看patient_view
```
SELECT *FROM patient_view_01;
```
<img width="916" alt="image" src="https://github.com/user-attachments/assets/6a9041d0-d4fe-4236-99e5-d15aa7113a3a" />

```
SELECT *FROM patient_view_02;
```
<img width="830" alt="image" src="https://github.com/user-attachments/assets/259c35d9-ef82-449c-8e3d-9e81924af0e0" />

```
SELECT *FROM patient_view_03;
```
<img width="833" alt="image" src="https://github.com/user-attachments/assets/9b40971d-7229-447e-a5e5-c86031d4a07b" />

```
SELECT *FROM patient_view_04;
```
<img width="832" alt="image" src="https://github.com/user-attachments/assets/7c8e3ec6-69b8-44f9-8989-080d31e3de30" />

```
SELECT *FROM patient_view_05;
```
<img width="839" alt="image" src="https://github.com/user-attachments/assets/519dcf3b-74c0-4b5d-a5bd-4c9577e04bbc" />


```
SELECT *FROM patient_view_06;
```
<img width="835" alt="image" src="https://github.com/user-attachments/assets/74058f30-6e73-414b-a1b6-ba370f84d5a8" />


```
SELECT *FROM patient_view_07;
```
<img width="832" alt="image" src="https://github.com/user-attachments/assets/2c5e382c-4e5d-42a5-9843-22cca0a335f2" />


```
SELECT *FROM patient_view_08;
```
<img width="832" alt="image" src="https://github.com/user-attachments/assets/ea698aee-652a-4e53-89fb-ab67ac04491e" />


```
SELECT *FROM patient_view_09;
```
<img width="829" alt="image" src="https://github.com/user-attachments/assets/e28bd74c-5ba3-40fa-9bc1-14dfa3597328" />


```
SELECT *FROM patient_view_10;
```
<img width="830" alt="image" src="https://github.com/user-attachments/assets/05255a6d-0017-45fa-88ce-ce0db2f665ac" />


```
SELECT *FROM patient_view_11;
```
<img width="830" alt="image" src="https://github.com/user-attachments/assets/4d14ea6d-c2f2-4669-a582-b8749454e184" />


```
SELECT *FROM patient_view_12;
```
<img width="824" alt="image" src="https://github.com/user-attachments/assets/53cc747f-d8bb-4eb4-a339-3ee696c678ba" />


```
SELECT *FROM patient_view_13;
```
<img width="829" alt="image" src="https://github.com/user-attachments/assets/01444389-dc54-49f7-8fa1-ef5ab91c6327" />


```
SELECT *FROM patient_view_14;
```
<img width="832" alt="image" src="https://github.com/user-attachments/assets/a671d916-eddf-40db-91f4-9825fbaf3504" />


```
SELECT *FROM patient_view_15;
```
<img width="832" alt="image" src="https://github.com/user-attachments/assets/2de9d2b9-1832-4f1d-ac30-c3592490911a" />



## 病人可以查看自己的個人資料
```
CREATE OR REPLACE VIEW patient_information_view_01 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號
FROM patient p
WHERE p.patient_id = 'P-2024-01';
```
```
CREATE OR REPLACE VIEW patient_information_view_02 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號
FROM patient p
WHERE p.patient_id = 'P-2024-02';
```
```
CREATE OR REPLACE VIEW patient_information_view_03 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號
FROM patient p
WHERE p.patient_id = 'P-2024-03';
```
```
CREATE OR REPLACE VIEW patient_information_view_04 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號
FROM patient p
WHERE p.patient_id = 'P-2024-04';
```
```
CREATE OR REPLACE VIEW patient_information_view_05 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號
FROM patient p
WHERE p.patient_id = 'P-2024-05';
```
```
CREATE OR REPLACE VIEW patient_information_view_06 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號
FROM patient p
WHERE p.patient_id = 'P-2024-06';
```
```
CREATE OR REPLACE VIEW patient_information_view_07 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號
FROM patient p
WHERE p.patient_id = 'P-2024-07';
```
```
CREATE OR REPLACE VIEW patient_information_view_08 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號
FROM patient p
WHERE p.patient_id = 'P-2024-08';
```
```
CREATE OR REPLACE VIEW patient_information_view_09 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號
FROM patient p
WHERE p.patient_id = 'P-2024-09';
```
```
CREATE OR REPLACE VIEW patient_information_view_10 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號
FROM patient p
WHERE p.patient_id = 'P-2024-10';
```

```
CREATE OR REPLACE VIEW patient_information_view_11 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號
FROM patient p
WHERE p.patient_id = 'P-2024-11';
```
```
CREATE OR REPLACE VIEW patient_information_view_12 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號
FROM patient p
WHERE p.patient_id = 'P-2024-12';
```
```
CREATE OR REPLACE VIEW patient_information_view_13 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號
FROM patient p
WHERE p.patient_id = 'P-2024-13';
```
```
CREATE OR REPLACE VIEW patient_information_view_14 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號
FROM patient p
WHERE p.patient_id = 'P-2024-14';
```
```
CREATE OR REPLACE VIEW patient_information_view_15 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號
FROM patient p
WHERE p.patient_id = 'P-2024-15';
```

## 設定patient_information_view權限
```
GRANT SELECT ON hos.patient_information_view_01 TO 'patient_P_2024_01'@'localhost';
GRANT SELECT ON hos.patient_information_view_02 TO 'patient_P_2024_01'@'localhost';
GRANT SELECT ON hos.patient_information_view_03 TO 'patient_P_2024_01'@'localhost';
GRANT SELECT ON hos.patient_information_view_04 TO 'patient_P_2024_01'@'localhost';
GRANT SELECT ON hos.patient_information_view_05 TO 'patient_P_2024_01'@'localhost';
GRANT SELECT ON hos.patient_information_view_06 TO 'patient_P_2024_01'@'localhost';
GRANT SELECT ON hos.patient_information_view_07 TO 'patient_P_2024_01'@'localhost';
GRANT SELECT ON hos.patient_information_view_08 TO 'patient_P_2024_01'@'localhost';
GRANT SELECT ON hos.patient_information_view_09 TO 'patient_P_2024_01'@'localhost';
GRANT SELECT ON hos.patient_information_view_10 TO 'patient_P_2024_01'@'localhost';
GRANT SELECT ON hos.patient_information_view_11 TO 'patient_P_2024_01'@'localhost';
GRANT SELECT ON hos.patient_information_view_12 TO 'patient_P_2024_01'@'localhost';
GRANT SELECT ON hos.patient_information_view_13 TO 'patient_P_2024_01'@'localhost';
GRANT SELECT ON hos.patient_information_view_14 TO 'patient_P_2024_01'@'localhost';
GRANT SELECT ON hos.patient_information_view_15 TO 'patient_P_2024_01'@'localhost';
```

## 查看patient_information_view結果
```
SELECT *FROM patient_information_view_01;
```
<img width="436" alt="image" src="https://github.com/user-attachments/assets/5efb9b22-3c54-4819-ad24-2593f404fbc0" />

```
SELECT *FROM patient_information_view_02;
```
<img width="437" alt="image" src="https://github.com/user-attachments/assets/8ad83c33-61c8-47c7-9eb8-7ac188620936" />


```
SELECT *FROM patient_information_view_03;
```

<img width="433" alt="image" src="https://github.com/user-attachments/assets/5c65ea46-d067-430d-86c3-48931435995c" />


```
SELECT *FROM patient_information_view_04;
```
<img width="438" alt="image" src="https://github.com/user-attachments/assets/99346b5c-2ae6-44e4-843a-86dc3b94a718" />


```
SELECT *FROM patient_information_view_05;
```
<img width="433" alt="image" src="https://github.com/user-attachments/assets/e6fba5e9-3166-4490-b12e-dd09be9e6d31" />


```
SELECT *FROM patient_information_view_06;
```
<img width="434" alt="image" src="https://github.com/user-attachments/assets/15eb7a6d-9eb4-49f1-a43d-08afd0d1482d" />


```
SELECT *FROM patient_information_view_07;
```
<img width="434" alt="image" src="https://github.com/user-attachments/assets/c85d4895-88cd-4f2a-bf86-93d3d0925bca" />


```
SELECT *FROM patient_information_view_08;
```
<img width="438" alt="image" src="https://github.com/user-attachments/assets/94ddbdc5-38d6-478c-bbbd-de8ae7b330d4" />


```
SELECT *FROM patient_information_view_09;
```
<img width="437" alt="image" src="https://github.com/user-attachments/assets/0f7a2335-5e79-404a-810c-3acb5fa83099" />


```
SELECT *FROM patient_information_view_10;
```
<img width="434" alt="image" src="https://github.com/user-attachments/assets/79a8a1a2-ab58-4e8c-b64d-81c9ea0c1a5b" />


```
SELECT *FROM patient_information_view_11;
```
<img width="436" alt="image" src="https://github.com/user-attachments/assets/222c57b2-c6ba-4d45-a4b2-2ea85e1ee916" />


```
SELECT *FROM patient_information_view_12;
```
<img width="431" alt="image" src="https://github.com/user-attachments/assets/ca12efe9-1eff-4331-b2cd-a2d79d10e450" />


```
SELECT *FROM patient_information_view_13;
```
<img width="435" alt="image" src="https://github.com/user-attachments/assets/136a8414-fc48-4b42-9280-f958e4b7c5c0" />


```
SELECT *FROM patient_information_view_14;
```
<img width="435" alt="image" src="https://github.com/user-attachments/assets/06654bcf-0f19-45a6-a2e6-3610317907cd" />


```
SELECT *FROM patient_information_view_15;
```
<img width="436" alt="image" src="https://github.com/user-attachments/assets/79f06cce-2e9f-4977-8db2-b25719e1f425" />





























## 作業(Customer order entry)
```
CREATE TABLE Customer (
	customerNo INT PRIMARY KEY,
	customerName VARCHAR(255) NOT NULL,
	customerStreet VARCHAR(255),
	customerCity VARCHAR(255),
	customerState VARCHAR(255),
	customerZipCode VARCHAR(20),
	custTelNo VARCHAR(20),
	custFaxNo VARCHAR(20),
	DOB DATE,
	maritalStatus VARCHAR(20),
	creditRating VARCHAR(20)
);
```
```
INSERT INTO Customer (customerNo, customerName, customerStreet, customerCity, customerState, customerZipCode, custTelNo, custFaxNo, DOB, maritalStatus, creditRating) VALUES
(1, '張三', '中山路一段100號', '台北市', '台北', '10000', '02-23456789', '02-23456788', '1980-05-15', '未婚', 'AA'),
(2, '李四', '中正路二段200號', '台中市', '台中', '40000', '04-87654321', '04-87654322', '1975-10-20', '已婚', 'A'),
(3, '王五', '中華路三段300號', '台南市', '台南', '70000', '06-27890123', '06-27890124', '1990-03-01', '未婚', 'BBB'),
(4, '陳六', '自由路一段400號', '高雄市', '高雄', '80000', '07-23678901', '07-23678902', '1985-07-10', '已婚', 'A'),
(5, '林七', '和平路二段500號', '桃園市', '桃園', '33000', '03-23987654', '03-23987655', '1992-12-05', '未婚', 'BB');
```
![image](https://github.com/user-attachments/assets/59d4cb46-e496-470c-a126-c0f16c0f1168)

```
CREATE TABLE Employee (
	employeeNo INT PRIMARY KEY,
	title VARCHAR(10),
	firstName VARCHAR(50),
	middleName VARCHAR(50),
	lastName VARCHAR(50),
	address VARCHAR(255),
	workTelExt VARCHAR(20),
	homeTelNo VARCHAR(20),
	empEmailAddress VARCHAR(255),
	socialSecurityNumber VARCHAR(20),
	DOB DATE,
	position VARCHAR(100),
	sex VARCHAR(10),
	salary DECIMAL(10, 2),
	dateStarted DATE
);
```
```
INSERT INTO Employee (employeeNo, title, firstName, middleName, lastName, address, workTelExt, homeTelNo, empEmailAddress, socialSecurityNumber, DOB, position, sex, salary, dateStarted) VALUES
(101, '經理', '陳', NULL, '大文', '中山路一段100號, 台北市, 台灣', '1234', '02-9876543210', 'john.smith@example.com', 'SSN12345', '1970-01-15', '經理', '男', 50000.00, '2005-08-20'),
(102, '專員', '林', NULL, '靜宜', '忠孝東路二段200號, 台北市, 台灣', '5678', '02-9876543211', 'jane.doe@example.com', 'SSN67890', '1985-06-22', '專員', '女', 40000.00, '2010-03-01'),
(103, '工程師', '黃', NULL, '志明', '中正路三段300號, 台中市, 台灣', '9012', '04-9876543212', 'david.johnson@example.com', 'SSN23456', '1992-09-10', '工程師', '男', 60000.00, '2015-11-18'),
(104, '分析師', '張', NULL, '淑芬', '自由路一段400號, 高雄市, 台灣', '3456', '07-9876543213', 'sarah.williams@example.com', 'SSN78901', '1988-04-03', '分析師', '女', 45000.00, '2012-07-05'),
(105, '技術員', '李', NULL, '國華', '和平路二段500號, 桃園市, 台灣', '7890', '03-9876543214', 'michael.brown@example.com', 'SSN34567', '1995-02-28', '技術員', '男', 35000.00, '2018-09-24');
```
![image](https://github.com/user-attachments/assets/897b3e81-9d2b-4f50-93f9-c74663a7181a)

```
CREATE TABLE `Order` (
	orderNo INT PRIMARY KEY,
	orderDate DATE,
	billingStreet VARCHAR(255),
	billingCity VARCHAR(255),
	billingState VARCHAR(255),
	billingZipCode VARCHAR(20),
	promisedDate DATE,
	status VARCHAR(20),
	customerNo INT,
	employeeNo INT,
	FOREIGN KEY (customerNo) REFERENCES Customer(customerNo),
	FOREIGN KEY (employeeNo) REFERENCES Employee(employeeNo)
);
```
```
INSERT INTO `Order` (orderNo, orderDate, billingStreet, billingCity, billingState, billingZipCode, promisedDate, status, customerNo, employeeNo) VALUES
(2001, '2023-01-20', '中山路一段100號', '台北市', '台北', '10000', '2023-01-27', '已出貨', 1, 101),
(2002, '2023-02-05', '忠孝東路二段200號', '台北市', '台北', '10600', '2023-02-12', '已出貨', 2, 102),
(2003, '2023-02-25', '中正路三段300號', '台中市', '台中', '40000', '2023-03-04', '處理中', 3, 103),
(2004, '2023-03-10', '自由路一段400號', '高雄市', '高雄', '80000', '2023-03-17', '已出貨', 4, 101),
(2005, '2023-03-28', '和平路二段500號', '桃園市', '桃園', '33000', '2023-04-04', '處理中', 5, 102);
```
![image](https://github.com/user-attachments/assets/8da0760d-e9a7-468a-aee0-cf8973f56478)

```
CREATE TABLE PaymentMethod (
	pMethodNo INT PRIMARY KEY,
	paymentMethod VARCHAR(255)
);
```
```
INSERT INTO PaymentMethod (pMethodNo, paymentMethod) VALUES
(3001, '信用卡'),
(3002, '現金'),
(3003, '支票'),
(3004, '銀行轉帳'),
(3005, '行動支付');
```
![image](https://github.com/user-attachments/assets/9c22613c-7d87-421a-931f-c153a5e3bb8b)

```
CREATE TABLE Invoice (
	invoiceNo INT PRIMARY KEY,
	dateRaised DATE,
	datePaid DATE,
	creditCardNo VARCHAR(20),
	holdersName VARCHAR(255),
	expiryDate DATE,
	orderNo INT,
	pMethodNo INT,
	FOREIGN KEY (orderNo) REFERENCES `Order`(orderNo),
	FOREIGN KEY (pMethodNo) REFERENCES PaymentMethod(pMethodNo)
);
```
```
INSERT INTO Invoice (invoiceNo, dateRaised, datePaid, creditCardNo, holdersName, expiryDate, orderNo, pMethodNo) VALUES
(1001, '2023-01-25', '2023-01-25', '1234567890123456', '張三', '2028-12-31', 2001, 3001),
(1002, '2023-02-10', '2023-02-15', '9876543210987654', '李四', '2027-11-30', 2002, 3002),
(1003, '2023-03-01', '2023-03-05', '5678901234567890', '王五', '2029-05-31', 2003, 3003),
(1004, '2023-03-15', '2023-03-20', '0987654321098765', '陳六', '2028-08-31', 2004, 3001),
(1005, '2023-04-01', '2023-04-05', '4321098765432109', '林七', '2027-10-31', 2005, 3002);
```
![image](https://github.com/user-attachments/assets/448a4920-6465-4d0c-af8e-f8e3a4b36502)

```
CREATE TABLE Product (
	productNo INT PRIMARY KEY,
	productName VARCHAR(255) NOT NULL,
	serialNo VARCHAR(255),
	unitPrice DECIMAL(10, 2),
	quantityOnHand INT,
	reorderLevel INT,
	reorderQuantity INT,
	reorderLeadTime INT
);
```
```
INSERT INTO Product (productNo, productName, serialNo, unitPrice, quantityOnHand, reorderLevel, reorderQuantity, reorderLeadTime) VALUES
(3001, '產品 A', 'SN-12345', 100.00, 50, 10, 100, 7),
(3002, '產品 B', 'SN-67890', 150.00, 30, 5, 50, 10),
(3003, '產品 C', 'SN-24680', 200.00, 20, 3, 30, 14),
(3004, '產品 D', 'SN-13579', 120.00, 40, 8, 80, 7),
(3005, '產品 E', 'SN-86420', 180.00, 25, 6, 60, 10);
```
![image](https://github.com/user-attachments/assets/266e0c82-f7c8-443a-9e92-a68d17acad0b)

```
CREATE TABLE OrderDetail (
	orderNo INT,
	productNo INT,
	quantityOrdered INT,
	PRIMARY KEY (orderNo, productNo),
	FOREIGN KEY (orderNo) REFERENCES `Order`(orderNo),
	FOREIGN KEY (productNo) REFERENCES Product(productNo)
);
```
```
INSERT INTO OrderDetail (orderNo, productNo, quantityOrdered) VALUES
(2001, 3001, 2),
(2001, 3002, 1),
(2002, 3003, 3),
(2003, 3001, 1),
(2003, 3004, 2);
```
![image](https://github.com/user-attachments/assets/bf424799-4ee4-489f-863e-cbff212fafc2)

```
CREATE TABLE ShipmentMethod (
	sMethodNo INT PRIMARY KEY,
	shipmentMethod VARCHAR(255)
);
```
```
INSERT INTO ShipmentMethod (sMethodNo, shipmentMethod) VALUES
(5001, '快遞'),
(5002, '郵寄'),
(5003, '貨運'),
(5004, '自取'),
(5005, '航空');
```
![image](https://github.com/user-attachments/assets/d48cf2e6-db45-4989-9357-0616a5eefac6)

```
CREATE TABLE Shipment (
	shipmentNo INT PRIMARY KEY,
	quantity INT,
	shipmentDate DATE,
	completeStatus VARCHAR(20),
	orderNo INT,
	productNo INT,
	employeeNo INT,
	sMethodNo INT,
	FOREIGN KEY (orderNo, productNo) REFERENCES OrderDetail(orderNo, productNo),
	FOREIGN KEY (employeeNo) REFERENCES Employee(employeeNo),
	FOREIGN KEY (sMethodNo) REFERENCES ShipmentMethod(sMethodNo)
);
```
```
INSERT INTO Shipment (shipmentNo, quantity, shipmentDate, completeStatus, orderNo, productNo, employeeNo, sMethodNo) VALUES
(4001, 2, '2023-01-27', '完成', 2001, 3001, 101, 5001),
(4002, 1, '2023-02-12', '完成', 2001, 3002, 102, 5002),
(4003, 1, '2023-03-04', '未完成', 2002, 3003, 103, 5001),
(4004, 2, '2023-03-17', '完成', 2003, 3001, 101, 5002),
(4005, 1, '2023-04-04', '未完成', 2003, 3004, 102, 5001);
```
![image](https://github.com/user-attachments/assets/e6bf2319-768b-4156-a69f-9762e15252fc)


## 作業(Inventory control)
```
CREATE TABLE Employee (
    employeeNo INT PRIMARY KEY,
    firstName VARCHAR(255),
    lastName VARCHAR(255)
);
```
```
INSERT INTO Employee (employeeNo, firstName, lastName) VALUES
    (1, '陳', '大文'),
    (2, '林', '靜宜'),
    (3, '黃', '志明'),
    (4, '張', '淑芬'),
    (5, '李', '國華');
```
![image](https://github.com/user-attachments/assets/0150607e-0b8d-4320-a3b4-f492fef873cc)

```
CREATE TABLE ProductCategory (
    categoryNo INT PRIMARY KEY,
    categoryDescription VARCHAR(255)
);
```
```
INSERT INTO ProductCategory (categoryNo, categoryDescription) VALUES
    (101, '服裝'),
    (102, '食品'),
    (103, '電子產品'),
    (104, '書籍'),
    (105, '家具');
```
![image](https://github.com/user-attachments/assets/96a99e1e-da6b-4617-8ccd-b28665d7f5c7)

```
CREATE TABLE Supplier (
    supplierNo INT PRIMARY KEY,
    supplierName VARCHAR(255),
    supplierStreet VARCHAR(255),
    supplierCity VARCHAR(255),
    supplierState VARCHAR(255),
    supplierZipCode VARCHAR(20),
    suppTelNo VARCHAR(20),
    suppFaxNo VARCHAR(20),
    suppEmailAddress VARCHAR(255),
    suppWebAddress VARCHAR(255),
    contactName VARCHAR(255),
    contactTelNo VARCHAR(20),
    contactFaxNo VARCHAR(20),
    contactEmailAddress VARCHAR(255),
    paymentTerms VARCHAR(255)
);
```
```
INSERT INTO Supplier (supplierNo, supplierName, supplierStreet, supplierCity, supplierState, supplierZipCode, suppTelNo, suppFaxNo, suppEmailAddress, suppWebAddress, contactName, contactTelNo, contactFaxNo, contactEmailAddress, paymentTerms) VALUES
    (201, 'AAA公司', '中山路一段100號', '台北市', '台北', '10000', '02-23456789', '02-23456788', 'abc@example.com', 'www.abccorp.com', '陳經理', '02-98765432', '02-98765433', 'contactA@example.com', '貨到付款'),
    (202, 'BBB公司', '中正路二段200號', '台中市', '台中', '40000', '04-22256789', '04-22256788', 'xyz@example.com', 'www.xyzinc.com', '林經理', '04-98765431', '04-98765432', 'contactB@example.com', '30天'),
    (203, 'CCC公司', '中華路三段300號', '台南市', '台南', '70000', '06-22890123', '06-22890124', 'pqr@example.com', 'www.pqrco.com', '黃經理', '06-98765430', '06-98765431', 'contactC@example.com', '60天'),
    (204, 'DDD有限公司', '自由路一段400號', '高雄市', '高雄', '80000', '07-23678901', '07-23678902', 'lmn@example.com', 'www.lmnltd.com', '張經理', '07-98765429', '07-98765430', 'contactD@example.com', '90天'),
    (205, 'EEE公司', '和平路二段500號', '桃園市', '桃園', '33000', '03-23987654', '03-23987655', 'rst@example.com', 'www.rstcorp.com', '李經理', '03-98765428', '03-98765429', 'contactE@example.com', '120天');
```
![image](https://github.com/user-attachments/assets/582de359-666c-47bf-9082-aa7c4640689a)

```
CREATE TABLE Product (
    productNo INT PRIMARY KEY,
    productName VARCHAR(255) NOT NULL,
    serialNo VARCHAR(255),
    unitPrice DECIMAL(10, 2),
    quantityOnHand INT,
    reorderLevel INT,
    reorderQuantity INT,
    reorderLeadTime INT,
    categoryNo INT,
    FOREIGN KEY (categoryNo) REFERENCES ProductCategory(categoryNo)
);
```
```
INSERT INTO Product (productNo, productName, serialNo, unitPrice, quantityOnHand, reorderLevel, reorderQuantity, reorderLeadTime, categoryNo) VALUES
    (301, 'Ｔ恤', 'TS12345', 15.99, 100, 20, 50, 7, 101),
    (302, '牛仔褲', 'JN67890', 29.99, 50, 10, 30, 14, 101),
    (303, '筆記型電腦', 'LP24680', 799.00, 20, 5, 10, 21, 103),
    (304, '書', 'BK13579', 19.95, 100, 25, 75, 7, 104),
    (305, '椅子', 'CH86420', 75.00, 30, 10, 20, 14, 105);
```
![image](https://github.com/user-attachments/assets/0e692138-f302-49ee-835b-9f4723108131)

```
CREATE TABLE PurchaseOrder (
    purchaseOrderNo INT PRIMARY KEY,
    purchaseOrderDescription VARCHAR(255),
    orderDate DATE,
    dateRequired DATE,
    shippedDate DATE,
    freightCharge DECIMAL(10, 2),
    supplierNo INT,
    employeeNo INT,
    FOREIGN KEY (supplierNo) REFERENCES Supplier(supplierNo),
    FOREIGN KEY (employeeNo) REFERENCES Employee(employeeNo)
);
```
```
INSERT INTO PurchaseOrder (purchaseOrderNo, purchaseOrderDescription, orderDate, dateRequired, shippedDate, freightCharge, supplierNo, employeeNo) VALUES
    (401, 'Ｔ恤訂單', '2024-01-10', '2024-01-20', '2024-01-18', 10.00, 201, 1),
    (402, '牛仔褲訂單', '2024-01-15', '2024-01-25', '2024-01-23', 15.00, 201, 2),
    (403, '筆記型電腦訂單', '2024-02-01', '2024-02-15', '2024-02-10', 25.00, 203, 3),
    (404, '書本訂單', '2024-02-05', '2024-02-15', '2024-02-12', 5.00, 204, 4),
    (405, '椅子訂單', '2024-02-10', '2024-02-20', '2024-02-18', 20.00, 205, 5);
```
![image](https://github.com/user-attachments/assets/6a19d32b-fd7d-4810-a786-cffee73150fd)

```
CREATE TABLE `Transaction` (
    transactionNo INT PRIMARY KEY,
    transactionDate DATE,
    transactionDescription VARCHAR(255),
    unitPrice DECIMAL(10, 2),
    unitsOrdered INT,
    unitsReceived INT,
    unitsSold INT,
    unitsWastage INT,
    productNo INT,
    purchaseOrderNo INT,
    FOREIGN KEY (productNo) REFERENCES Product(productNo),
    FOREIGN KEY (purchaseOrderNo) REFERENCES PurchaseOrder(purchaseOrderNo)
);
```
```
INSERT INTO `Transaction` (transactionNo, transactionDate, transactionDescription, unitPrice, unitsOrdered, unitsReceived, unitsSold, unitsWastage, productNo, purchaseOrderNo) VALUES
    (501, '2024-01-18', 'Ｔ恤購買交易', 15.99, 100, 100, 80, 0, 301, 401),
    (502, '2024-01-23', '牛仔褲購買交易', 29.99, 50, 50, 40, 0, 302, 402),
    (503, '2024-02-10', '筆記型電腦購買交易', 799.00, 10, 10, 5, 0, 303, 403),
    (504, '2024-02-12', '書本購買交易', 19.95, 75, 75, 60, 0, 304, 404),
    (505, '2024-02-18', '椅子購買交易', 75.00, 20, 20, 10, 0, 305, 405);
```
![image](https://github.com/user-attachments/assets/b4c75724-0f2a-428e-ab8d-6f51004d60dc)


## 簡報
https://www.canva.com/design/DAGj82tfSmY/Q-CFpZqbAzo32BPzIDAeGA/edit
