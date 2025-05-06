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
    patient_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL,
    phone VARCHAR(20),
    birth_date DATE,
    gender VARCHAR(2) CHECK (gender IN ('M', 'F')),
    national_id CHAR(10) UNIQUE,  
    resident_id CHAR(10) UNIQUE,  
    INDEX idx_patient_name (name),
    INDEX idx_birth_date (birth_date)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

## 醫生資料表
```
CREATE TABLE doctor (
    doctor_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL,
    specialty VARCHAR(50),
    phone VARCHAR(20),
    INDEX idx_doctor_specialty (specialty)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

## 病歷表
```
CREATE TABLE medical_record (
    medical_record_id INT PRIMARY KEY AUTO_INCREMENT,
    patient_id INT NOT NULL,
    diagnosis_record TEXT,
    last_visit_date DATE,
    FOREIGN KEY (patient_id) REFERENCES patient(patient_id) ON DELETE CASCADE,
    INDEX idx_last_visit (last_visit_date)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

## 預約表
```
CREATE TABLE appointment (
    appointment_id INT PRIMARY KEY AUTO_INCREMENT,
    medical_record_id INT NOT NULL,
    doctor_id INT NOT NULL,
    appointment_time DATETIME NOT NULL,
    status VARCHAR(20) DEFAULT 'scheduled',
    FOREIGN KEY (medical_record_id) REFERENCES medical_record(medical_record_id) ON DELETE CASCADE,
    FOREIGN KEY (doctor_id) REFERENCES doctor(doctor_id),
    INDEX idx_appointment_time (appointment_time),
    INDEX idx_status (status)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```
## 使用者帳號表
```
CREATE TABLE user (
    username VARCHAR(50) PRIMARY KEY,
    password VARCHAR(100) NOT NULL,
    user_type ENUM('patient', 'doctor', 'admin') NOT NULL,
    doctor_id INT,
    patient_id INT,
    medical_record_id INT,
    FOREIGN KEY (doctor_id) REFERENCES doctor(doctor_id),
    FOREIGN KEY (patient_id) REFERENCES patient(patient_id),
    FOREIGN KEY (medical_record_id) REFERENCES medical_record(medical_record_id),
    INDEX idx_user_type (user_type)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

## 新增病患資料
```
INSERT INTO patient (name, phone, birth_date, gender, national_id, resident_id) VALUES
('王小明', '0912345678', '1990-01-15', 'M', 'A123456789', NULL),
('李美麗', '0922333444', '1985-06-28', 'F', 'B223456789', NULL),
('陳建宏', '0933221144', '1975-12-02', 'M', 'C123456789', NULL),
('張凱婷', '0955667788', '1992-04-10', 'F', NULL, 'A800000001'),
('林靜怡', '0966112233', '2000-08-20', 'F', NULL, 'A900000002');
```

## 新增醫生資料
```
INSERT INTO doctor (name, specialty, phone) VALUES
('林文雄', '牙科矯正', '0288776655'),
('黃信誠', '口腔外科', '0277889900'),
('蔡宜君', '兒童牙科', '0222113344');
```

## 新增病歷資料
```
INSERT INTO medical_record (patient_id, diagnosis_record, last_visit_date) VALUES
(1, '蛀牙治療，補牙完成', '2024-12-15'),
(2, '智齒拔除後恢復良好', '2025-03-20'),
(3, '牙齒矯正第一階段結束', '2025-01-10');
```

## 新增預約表資料
```
INSERT INTO appointment (medical_record_id, doctor_id, appointment_time, status) VALUES
(1, 1, '2025-05-10 10:00:00', 'scheduled'),
(2, 2, '2025-05-08 14:00:00', 'completed'),
(3, 1, '2025-05-11 09:30:00', 'scheduled');
```

## 新增管理員帳號密碼資料
```
INSERT INTO user (username, password, user_type)
VALUES ('admin', 'admin123', 'admin');
```

## 新增醫生帳號密碼資料
```
INSERT INTO user (username, password, user_type, doctor_id)
SELECT
    CASE d.name
        WHEN '王大明' THEN 'dr_wang'
        WHEN '林小芳' THEN 'dr_lin1'
        WHEN '林文雄' THEN 'dr_lin2'
        WHEN '黃信誠' THEN 'dr_huang'
        WHEN '蔡宜君' THEN 'dr_tsai'
    END AS username,
    CASE d.name
        WHEN '王大明' THEN 'wang456'
        WHEN '林小芳' THEN 'lin789'
        WHEN '林文雄' THEN 'wen321'
        WHEN '黃信誠' THEN 'huang111'
        WHEN '蔡宜君' THEN 'tsai555'
    END AS password,
    'doctor',
    d.doctor_id
FROM doctor d
WHERE d.name IN ('王大明', '林小芳', '林文雄', '黃信誠', '蔡宜君');
```

## 新增病患帳號密碼資料
```
INSERT INTO user (username, password, user_type, patient_id)
SELECT
    CASE p.name
        WHEN '陳怡君' THEN 'pt_chen'
        WHEN '李志明' THEN 'pt_lee'
        WHEN '黃美惠' THEN 'pt_huang'
    END AS username,
    CASE p.name
        WHEN '陳怡君' THEN 'chen999'
        WHEN '李志明' THEN 'lee123'
        WHEN '黃美惠' THEN 'huang888'
    END AS password,
    'patient',
    p.patient_id
FROM patient p
WHERE p.name IN ('陳怡君', '李志明', '黃美惠');
```

## 建立檢視表為醫生可以看到的資訊
```
CREATE VIEW view_doctor_schedule AS
SELECT d.name AS doctor_name, p.name AS patient_name, a.appointment_time, mr.diagnosis_record
FROM appointment a
JOIN doctor d ON a.doctor_id = d.doctor_id
JOIN medical_record mr ON a.medical_record_id = mr.medical_record_id
JOIN patient p ON mr.patient_id = p.patient_id;
```

## 建立檢視表為管理員可以看到資訊
```
CREATE OR REPLACE VIEW view_user_summary AS
SELECT 
    -- 病患資訊
    p.patient_id,
    p.name AS patient_name,
    p.phone AS patient_phone,
    p.national_id,
    p.resident_id,
    
    -- 醫生資訊
    d.doctor_id,
    d.name AS doctor_name,
    d.specialty,
    d.phone AS doctor_phone

FROM user u
LEFT JOIN patient p ON u.patient_id = p.patient_id
LEFT JOIN doctor d ON u.doctor_id = d.doctor_id;
```

## 建立檢視表為病患可以看到的資訊
```
CREATE VIEW view_patient_record AS
SELECT u.username, p.name AS patient_name, mr.diagnosis_record, a.appointment_time
FROM user u
JOIN patient p ON u.patient_id = p.patient_id
JOIN medical_record mr ON mr.patient_id = p.patient_id
JOIN appointment a ON a.medical_record_id = mr.medical_record_id
WHERE u.user_type = 'patient';
```

## 簡報
https://www.canva.com/design/DAGj82tfSmY/Q-CFpZqbAzo32BPzIDAeGA/edit
