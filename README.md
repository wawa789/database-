## 組員

林國善
41136111 資訊工程系3年級乙班
製作github、Word製作

吳柏毅
41143262 資訊工程系3年級乙班
實作資料庫、製作報告

王馨卉
41146102 企業管理系3年級甲班
製作報告、錄製影片

# 題目 牙醫診所掛號管理資料庫系統

## 完整書面報告PDF

[第九組 資料庫期末專題.pdf](https://github.com/user-attachments/files/20743256/default.pdf)

## 簡報

https://www.canva.com/design/DAGj82tfSmY/Q-CFpZqbAzo32BPzIDAeGA/edit

## 實作影片

https://youtu.be/whEspVsIwd4?si=csXqtY7JaJ-Mum8-

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

![ER全圖A摘要圖](https://github.com/user-attachments/assets/16cbf35c-9718-4971-acd5-6f1e6e8d8b23)


詳細全圖

![ER全圖A](https://github.com/user-attachments/assets/ce6fbb7a-91e2-4de8-bf76-05e41e84bf7f)



病患

![病患](https://github.com/user-attachments/assets/6b6deb90-642a-43e3-a2b1-8bcabbef0df2)


醫生

![醫生](https://github.com/user-attachments/assets/ceccd1d2-5c1b-4851-9e5b-a9a8fd95f156)


病歷

![病例](https://github.com/user-attachments/assets/997b8afa-aa98-487d-a89f-ebe4aff9c4f5)


班表

![班表](https://github.com/user-attachments/assets/25095a56-f016-4936-bfba-183071bcf773)


診間

![診間](https://github.com/user-attachments/assets/baf61b58-cda7-4960-90a3-e9fc268dfdc8)


## 建立資料庫並使用
```
CREATE DATABASE hos;
USE hos;
```
## 病患資料表
```
CREATE OR REPLACE TABLE patient (
    patient_id VARCHAR(30) PRIMARY KEY,
    CHECK (patient_id REGEXP '^P-[0-9]{4}-[0-9]{2,3}$'),

    national_id CHAR(10) NOT NULL UNIQUE,
    CHECK (national_id REGEXP '^[A-Z][12][0-9]{8}$'),

    name TEXT NOT NULL,
    CHECK (name REGEXP '^[一-龥]+$'),

    gender TEXT CHECK (gender IN ('男', '女')),

    birth_date DATE,

    phone CHAR(10) NOT NULL UNIQUE,
    CHECK (phone REGEXP '^09[0-9]{8}$')
);
```

```
DELIMITER //

CREATE FUNCTION is_valid_national_id(id CHAR(10)) RETURNS BOOLEAN
DETERMINISTIC
BEGIN
    DECLARE letter_map CHAR(50) DEFAULT 'ABCDEFGHJKLMNPQRSTUVXYWZIO';
    DECLARE letter_index INT;
    DECLARE n1 INT;
    DECLARE sum INT;
    DECLARE i INT;

    IF id NOT REGEXP '^[A-Z][12][0-9]{8}$' THEN
        RETURN FALSE;
    END IF;

    SET letter_index = LOCATE(SUBSTRING(id, 1, 1), letter_map);
    IF letter_index = 0 THEN
        RETURN FALSE;
    END IF;

    SET n1 = CASE 
        WHEN SUBSTRING(id,1,1) = 'I' THEN 34
        WHEN SUBSTRING(id,1,1) = 'O' THEN 35
        WHEN SUBSTRING(id,1,1) = 'W' THEN 32
        WHEN SUBSTRING(id,1,1) = 'Z' THEN 33
        ELSE letter_index + 9
    END;

    SET sum = FLOOR(n1 / 10) * 1 + (n1 % 10) * 9;

    SET i = 2;
    WHILE i <= 9 DO
        SET sum = sum + CAST(SUBSTRING(id, i, 1) AS UNSIGNED) * (10 - i);
        SET i = i + 1;
    END WHILE;

    SET sum = sum + CAST(SUBSTRING(id, 10, 1) AS UNSIGNED);

    RETURN (MOD(sum, 10) = 0);
END;
//

DELIMITER ;
```
```
DELIMITER //

CREATE TRIGGER check_national_id_before_insert
BEFORE INSERT ON patient
FOR EACH ROW
BEGIN
    IF NOT is_valid_national_id(NEW.national_id) THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Invalid national ID format or checksum.';
    END IF;
END;
//

DELIMITER ;
```

## 醫生資料表
```
CREATE TABLE doctor (
    doctor_id VARCHAR(30) PRIMARY KEY,
    name TEXT NOT NULL,
    specialty TEXT NOT NULL,
    phone VARCHAR(10) NOT NULL UNIQUE
);

```
```
DELIMITER //

DROP TRIGGER IF EXISTS validate_doctor_before_insert;

CREATE TRIGGER validate_doctor_before_insert
BEFORE INSERT ON doctor
FOR EACH ROW
BEGIN
    IF NEW.doctor_id NOT REGEXP '^D-[0-9]{3}$' THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'doctor_id 格式錯誤，需為 D 開頭加上 3 位數字，如 D-001';
    END IF;

    IF NEW.name NOT REGEXP '^[一-龥]+$' THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'name 格式錯誤，只能輸入中文';
    END IF;

    IF NEW.specialty NOT REGEXP '^[一-龥]+$' THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'specialty 格式錯誤，只能輸入中文';
    END IF;

    IF NEW.phone NOT REGEXP '^09[0-9]{8}$' THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'phone 格式錯誤，需為 09 開頭共 10 位數字';
    END IF;
END;
//

DELIMITER ;
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
```
DELIMITER //

DROP TRIGGER IF EXISTS validate_medical_record_before_insert;

CREATE TRIGGER validate_medical_record_before_insert
BEFORE INSERT ON medical_record
FOR EACH ROW
BEGIN
    IF NEW.medical_record_id NOT REGEXP '^MR-[0-9]{3}$' THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'medical_record_id 格式錯誤，需為 MR 開頭加上 3 位數字，如 MR-001';
    END IF;

    IF NEW.diagnosis_record NOT REGEXP '^[一-龥]+$' THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'diagnosis_record 格式錯誤，僅允許中文';
    END IF;
    IF NEW.visits_date > CURDATE() THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'visits_date 不可晚於今天';
    END IF;
END;
//

DELIMITER ;
```



## 醫生排班表
```
CREATE OR REPLACE TABLE schedule (
    schedule_id INT PRIMARY KEY AUTO_INCREMENT,
    doctor_id VARCHAR(30) NOT NULL,
    schedule_date DATE NOT NULL,
    schedule_time VARCHAR(10) NOT NULL CHECK (schedule_time IN ('上午', '下午', '晚上')),
    week VARCHAR(10) NOT NULL CHECK (week IN ('一', '二', '三', '四', '五', '六', '日')),
    clinic VARCHAR(10) NOT NULL CHECK (clinic REGEXP '^[0-9]{3}診間$'),
    schedule_status VARCHAR(10) NOT NULL CHECK (schedule_status IN ('開診', '已滿', '休診')),
    
    FOREIGN KEY (doctor_id) REFERENCES doctor(doctor_id)
);

```
```
CREATE OR REPLACE TABLE schedule (
    schedule_id INT PRIMARY KEY AUTO_INCREMENT,

    doctor_id VARCHAR(30) NOT NULL,

    schedule_date DATE NOT NULL,

    schedule_time VARCHAR(10) NOT NULL 
        CHECK (schedule_time IN ('上午', '下午', '晚上')),

    week VARCHAR(10) NOT NULL 
        CHECK (week IN ('星期一', '星期二', '星期三', '星期四', '星期五', '星期六', '星期日')),

    clinic VARCHAR(10) NOT NULL
        CHECK (clinic REGEXP '^[1-9][0-9]{2}診間$'),

    schedule_status VARCHAR(10) NOT NULL 
        CHECK (schedule_status IN ('開診', '已滿', '休診')),

    FOREIGN KEY (doctor_id) REFERENCES doctor(doctor_id)
);
```
## 預約表
```
CREATE OR REPLACE TABLE appointment (
    appointment_id VARCHAR(30) PRIMARY KEY,
    patient_id VARCHAR(30) NOT NULL,
    doctor_id VARCHAR(30) NOT NULL,
    schedule_id INTEGER NOT NULL,
    number VARCHAR(10),
    status TEXT NOT NULL,
    medical_record_id VARCHAR(30),

    FOREIGN KEY (patient_id) REFERENCES patient(patient_id),
    FOREIGN KEY (doctor_id) REFERENCES doctor(doctor_id),
    FOREIGN KEY (schedule_id) REFERENCES schedule(schedule_id),
    FOREIGN KEY (medical_record_id) REFERENCES medical_record(medical_record_id),

    CHECK (appointment_id REGEXP '^[0-9]{4}-[0-9]{2}-[0-9]{2}-[0-9]{3}$'),

    CHECK (patient_id REGEXP '^P-[0-9]{4}-[0-9]{2,}$'),

    CHECK (number IS NULL OR number REGEXP '^[1-9][0-9]{0,2}號$'),

    CHECK (status IN ('已預約', '已完成', '取消'))
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


INSERT INTO appointment (
    appointment_id, patient_id, doctor_id, schedule_id, number, status, medical_record_id
) VALUES
('2025-04-21-001', 'P-2024-01', 'D-001', 1, '1號', '已完成', 'MR-001'),
('2025-04-22-002', 'P-2024-02', 'D-002', 2, '1號', '已預約', 'MR-002'),
('2025-04-23-003', 'P-2024-03', 'D-003', 3, NULL,  '取消', 'MR-003'),
('2025-04-24-004', 'P-2024-04', 'D-010', 10, '1號', '已完成', 'MR-004'),
('2025-04-25-005', 'P-2024-05', 'D-005', 5, '1號', '已預約', 'MR-005'),
('2025-04-26-006', 'P-2024-06', 'D-006', 6, '1號', '已完成', 'MR-006'),
('2025-04-27-007', 'P-2024-07', 'D-007', 7, '1號', '已預約', 'MR-007'),
('2025-04-28-008', 'P-2024-08', 'D-010', 10, '1號', '已完成', 'MR-008'),
('2025-04-29-009', 'P-2024-09', 'D-009', 9, '1號', '已預約', 'MR-009'),
('2025-04-30-010', 'P-2024-10', 'D-001', 1, '2號', '已完成', 'MR-010'),
('2025-05-01-011', 'P-2024-11', 'D-001', 1, '3號', '已預約', 'MR-011'),
('2025-05-02-012', 'P-2024-12', 'D-001', 1, '4號', '已預約', 'MR-012'),
('2025-05-03-013', 'P-2024-13', 'D-004', 4, NULL,  '取消', 'MR-013'),
('2025-05-04-014', 'P-2024-14', 'D-002', 2, '2號', '已預約', 'MR-014'),
('2025-05-05-015', 'P-2024-15', 'D-001', 1, '5號', '已預約', 'MR-015');

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
## 創建病患使用者
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


## 使用ID:P-2024-01登入
```
mysql -u patient_P_2024_01 -p -h localhost
```
## 查看patient_view
```
SELECT *FROM patient_view_01;
```
![image](https://github.com/user-attachments/assets/169ef5dd-a14a-4ccb-93cb-91a089646712)
```
SELECT *FROM patient_view_02;
```
![image](https://github.com/user-attachments/assets/b309e6cc-dfb9-4a09-9d33-2ee3c7a29bd7)
```
SELECT *FROM patient_view_03;
```
![image](https://github.com/user-attachments/assets/e617b8a0-b40f-400d-b3ce-9077997904db)
```
SELECT *FROM patient_view_04;
```
![image](https://github.com/user-attachments/assets/978ee969-8ebc-4310-8018-c3b2a308a00e)
```
SELECT *FROM patient_view_05;
```
![image](https://github.com/user-attachments/assets/2c92593d-6181-4c16-aaf1-9a207793fd79)
```
SELECT *FROM patient_view_06;
```
![image](https://github.com/user-attachments/assets/e07a5874-a4a5-4a4f-bfb9-e7e8712b8d90)
```
SELECT *FROM patient_view_07;
```
![image](https://github.com/user-attachments/assets/579fe47d-c02c-4733-a2dc-ef0a14baf06d)
```
SELECT *FROM patient_view_08;
```
![image](https://github.com/user-attachments/assets/fd2ed63a-e2d9-434a-adf8-dce60265da47)
```
SELECT *FROM patient_view_09;
```
![image](https://github.com/user-attachments/assets/520fdda7-021a-41d1-ad75-3e7cde811c04)
```
SELECT *FROM patient_view_10;
```
![image](https://github.com/user-attachments/assets/7cdd7701-4136-472a-9b13-c496cb0184ce)
```
SELECT *FROM patient_view_11;
```
![image](https://github.com/user-attachments/assets/ed6cbee0-09f3-439d-b299-9c135a89237d)
```
SELECT *FROM patient_view_12;
```
![image](https://github.com/user-attachments/assets/96cd7117-54ab-40b0-9ebd-e8676c902f59)
```
SELECT *FROM patient_view_13;
```
![image](https://github.com/user-attachments/assets/a956ebef-9f51-44af-bd18-e5c66f2f8c4c)
```
SELECT *FROM patient_view_14;
```
![image](https://github.com/user-attachments/assets/d1a1f263-5656-4852-a7f9-54e68ddadffc)
```
SELECT *FROM patient_view_15;
```
![image](https://github.com/user-attachments/assets/47c281ba-5b80-458b-a1e4-3808676b5765)


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
GRANT SELECT ON hos.patient_information_view_02 TO 'patient_P_2024_02'@'localhost';
GRANT SELECT ON hos.patient_information_view_03 TO 'patient_P_2024_03'@'localhost';
GRANT SELECT ON hos.patient_information_view_04 TO 'patient_P_2024_04'@'localhost';
GRANT SELECT ON hos.patient_information_view_05 TO 'patient_P_2024_05'@'localhost';
GRANT SELECT ON hos.patient_information_view_06 TO 'patient_P_2024_06'@'localhost';
GRANT SELECT ON hos.patient_information_view_07 TO 'patient_P_2024_07'@'localhost';
GRANT SELECT ON hos.patient_information_view_08 TO 'patient_P_2024_08'@'localhost';
GRANT SELECT ON hos.patient_information_view_09 TO 'patient_P_2024_09'@'localhost';
GRANT SELECT ON hos.patient_information_view_10 TO 'patient_P_2024_10'@'localhost';
GRANT SELECT ON hos.patient_information_view_11 TO 'patient_P_2024_11'@'localhost';
GRANT SELECT ON hos.patient_information_view_12 TO 'patient_P_2024_12'@'localhost';
GRANT SELECT ON hos.patient_information_view_13 TO 'patient_P_2024_13'@'localhost';
GRANT SELECT ON hos.patient_information_view_14 TO 'patient_P_2024_14'@'localhost';
GRANT SELECT ON hos.patient_information_view_15 TO 'patient_P_2024_15'@'localhost';
```

## 查看patient_information_view結果
```
SELECT *FROM patient_information_view_01;
```
![image](https://github.com/user-attachments/assets/0e0adee1-43a4-44a0-9eff-e4ad94c2d08c)

```
SELECT *FROM patient_information_view_02;
```
![image](https://github.com/user-attachments/assets/208d790b-1aff-413e-943c-bbc587722b68)

```
SELECT *FROM patient_information_view_03;
```
![image](https://github.com/user-attachments/assets/ec3b8285-3ca0-437e-93b4-895e50f55178)

```
SELECT *FROM patient_information_view_04;
```
![image](https://github.com/user-attachments/assets/5f242464-133e-4764-ae34-f5d6ffe11eca)

```
SELECT *FROM patient_information_view_05;
```
![image](https://github.com/user-attachments/assets/6cf2854b-eab0-4695-97f2-16edd245475a)

```
SELECT *FROM patient_information_view_06;
```
![image](https://github.com/user-attachments/assets/03ce63c4-23c5-4304-99e2-451d5bf0e640)

```
SELECT *FROM patient_information_view_07;
```
![image](https://github.com/user-attachments/assets/a30c209b-054c-478a-b956-7ea6ea7a0a00)

```
SELECT *FROM patient_information_view_08;
```
![image](https://github.com/user-attachments/assets/22005dac-7831-4e52-afdd-d766529ab8b5)

```
SELECT *FROM patient_information_view_09;
```
![image](https://github.com/user-attachments/assets/29de350b-5f08-45a0-a257-7867b9db1387)

```
SELECT *FROM patient_information_view_10;
```
![image](https://github.com/user-attachments/assets/3e37672c-26fb-4d49-8cb7-eeeaa3f3c090)

```
SELECT *FROM patient_information_view_11;
```
![image](https://github.com/user-attachments/assets/7ef3d12c-8115-4b12-8ef7-77673c271246)

```
SELECT *FROM patient_information_view_12;
```
![image](https://github.com/user-attachments/assets/789038d3-a1c5-4d30-852e-a668a2a66d75)

```
SELECT *FROM patient_information_view_13;
```
![image](https://github.com/user-attachments/assets/07ba818f-4669-4ee3-b09a-4bd7c91e8593)

```
SELECT *FROM patient_information_view_14;
```
![image](https://github.com/user-attachments/assets/d36ac3ff-f613-40fd-8f07-6924a22eb315)

```
SELECT *FROM patient_information_view_15;
```
![image](https://github.com/user-attachments/assets/0b907755-32fc-4907-b889-1679dd4bf4ea)



## 病人可以查看自己最新一筆的診斷紀錄
```
CREATE OR REPLACE VIEW patient_record_view_01 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號,
    mr.diagnosis_record AS 最新診斷,
    mr.visits_date AS 就診日期
FROM patient p
LEFT JOIN medical_record mr ON mr.medical_record_id = (
    SELECT medical_record_id 
    FROM medical_record 
    WHERE patient_id = p.patient_id 
    ORDER BY visits_date DESC 
    LIMIT 1
)
WHERE p.patient_id = 'P-2024-01';
```
```
CREATE OR REPLACE VIEW patient_record_view_02 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號,
    mr.diagnosis_record AS 最新診斷,
    mr.visits_date AS 就診日期
FROM patient p
LEFT JOIN medical_record mr ON mr.medical_record_id = (
    SELECT medical_record_id 
    FROM medical_record 
    WHERE patient_id = p.patient_id 
    ORDER BY visits_date DESC 
    LIMIT 1
)
WHERE p.patient_id = 'P-2024-02';
```
```
CREATE OR REPLACE VIEW patient_record_view_03 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號,
    mr.diagnosis_record AS 最新診斷,
    mr.visits_date AS 就診日期
FROM patient p
LEFT JOIN medical_record mr ON mr.medical_record_id = (
    SELECT medical_record_id 
    FROM medical_record 
    WHERE patient_id = p.patient_id 
    ORDER BY visits_date DESC 
    LIMIT 1
)
WHERE p.patient_id = 'P-2024-03';
```
```
CREATE OR REPLACE VIEW patient_record_view_04 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號,
    mr.diagnosis_record AS 最新診斷,
    mr.visits_date AS 就診日期
FROM patient p
LEFT JOIN medical_record mr ON mr.medical_record_id = (
    SELECT medical_record_id 
    FROM medical_record 
    WHERE patient_id = p.patient_id 
    ORDER BY visits_date DESC 
    LIMIT 1
)
WHERE p.patient_id = 'P-2024-04';
```
```
CREATE OR REPLACE VIEW patient_record_view_05 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號,
    mr.diagnosis_record AS 最新診斷,
    mr.visits_date AS 就診日期
FROM patient p
LEFT JOIN medical_record mr ON mr.medical_record_id = (
    SELECT medical_record_id 
    FROM medical_record 
    WHERE patient_id = p.patient_id 
    ORDER BY visits_date DESC 
    LIMIT 1
)
WHERE p.patient_id = 'P-2024-05';
```
```
CREATE OR REPLACE VIEW patient_record_view_06 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號,
    mr.diagnosis_record AS 最新診斷,
    mr.visits_date AS 就診日期
FROM patient p
LEFT JOIN medical_record mr ON mr.medical_record_id = (
    SELECT medical_record_id 
    FROM medical_record 
    WHERE patient_id = p.patient_id 
    ORDER BY visits_date DESC 
    LIMIT 1
)
WHERE p.patient_id = 'P-2024-06';
```
```
CREATE OR REPLACE VIEW patient_record_view_07 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號,
    mr.diagnosis_record AS 最新診斷,
    mr.visits_date AS 就診日期
FROM patient p
LEFT JOIN medical_record mr ON mr.medical_record_id = (
    SELECT medical_record_id 
    FROM medical_record 
    WHERE patient_id = p.patient_id 
    ORDER BY visits_date DESC 
    LIMIT 1
)
WHERE p.patient_id = 'P-2024-07';
```
```
CREATE OR REPLACE VIEW patient_record_view_08 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號,
    mr.diagnosis_record AS 最新診斷,
    mr.visits_date AS 就診日期
FROM patient p
LEFT JOIN medical_record mr ON mr.medical_record_id = (
    SELECT medical_record_id 
    FROM medical_record 
    WHERE patient_id = p.patient_id 
    ORDER BY visits_date DESC 
    LIMIT 1
)
WHERE p.patient_id = 'P-2024-08';
```
```
CREATE OR REPLACE VIEW patient_record_view_09 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號,
    mr.diagnosis_record AS 最新診斷,
    mr.visits_date AS 就診日期
FROM patient p
LEFT JOIN medical_record mr ON mr.medical_record_id = (
    SELECT medical_record_id 
    FROM medical_record 
    WHERE patient_id = p.patient_id 
    ORDER BY visits_date DESC 
    LIMIT 1
)
WHERE p.patient_id = 'P-2024-09';
```
```
CREATE OR REPLACE VIEW patient_record_view_10 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號,
    mr.diagnosis_record AS 最新診斷,
    mr.visits_date AS 就診日期
FROM patient p
LEFT JOIN medical_record mr ON mr.medical_record_id = (
    SELECT medical_record_id 
    FROM medical_record 
    WHERE patient_id = p.patient_id 
    ORDER BY visits_date DESC 
    LIMIT 1
)
WHERE p.patient_id = 'P-2024-10';
```
```
CREATE OR REPLACE VIEW patient_record_view_11 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號,
    mr.diagnosis_record AS 最新診斷,
    mr.visits_date AS 就診日期
FROM patient p
LEFT JOIN medical_record mr ON mr.medical_record_id = (
    SELECT medical_record_id 
    FROM medical_record 
    WHERE patient_id = p.patient_id 
    ORDER BY visits_date DESC 
    LIMIT 1
)
WHERE p.patient_id = 'P-2024-11';
```
```
CREATE OR REPLACE VIEW patient_record_view_12 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號,
    mr.diagnosis_record AS 最新診斷,
    mr.visits_date AS 就診日期
FROM patient p
LEFT JOIN medical_record mr ON mr.medical_record_id = (
    SELECT medical_record_id 
    FROM medical_record 
    WHERE patient_id = p.patient_id 
    ORDER BY visits_date DESC 
    LIMIT 1
)
WHERE p.patient_id = 'P-2024-12';
```
```
CREATE OR REPLACE VIEW patient_record_view_13 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號,
    mr.diagnosis_record AS 最新診斷,
    mr.visits_date AS 就診日期
FROM patient p
LEFT JOIN medical_record mr ON mr.medical_record_id = (
    SELECT medical_record_id 
    FROM medical_record 
    WHERE patient_id = p.patient_id 
    ORDER BY visits_date DESC 
    LIMIT 1
)
WHERE p.patient_id = 'P-2024-13';
```
```
CREATE OR REPLACE VIEW patient_record_view_14 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號,
    mr.diagnosis_record AS 最新診斷,
    mr.visits_date AS 就診日期
FROM patient p
LEFT JOIN medical_record mr ON mr.medical_record_id = (
    SELECT medical_record_id 
    FROM medical_record 
    WHERE patient_id = p.patient_id 
    ORDER BY visits_date DESC 
    LIMIT 1
)
WHERE p.patient_id = 'P-2024-14';
```
```
CREATE OR REPLACE VIEW patient_record_view_15 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 病人出生年月日,
    p.phone AS 病人電話,
    p.national_id AS 病人身分證字號,
    mr.diagnosis_record AS 最新診斷,
    mr.visits_date AS 就診日期
FROM patient p
LEFT JOIN medical_record mr ON mr.medical_record_id = (
    SELECT medical_record_id 
    FROM medical_record 
    WHERE patient_id = p.patient_id 
    ORDER BY visits_date DESC 
    LIMIT 1
)
WHERE p.patient_id = 'P-2024-15';
```

## 設定patient_record_view權限

```
GRANT SELECT ON hos.patient_record_view_01 TO 'patient_P_2024_01'@'localhost';
GRANT SELECT ON hos.patient_record_view_02 TO 'patient_P_2024_02'@'localhost';
GRANT SELECT ON hos.patient_record_view_03 TO 'patient_P_2024_03'@'localhost';
GRANT SELECT ON hos.patient_record_view_04 TO 'patient_P_2024_04'@'localhost';
GRANT SELECT ON hos.patient_record_view_05 TO 'patient_P_2024_05'@'localhost';
GRANT SELECT ON hos.patient_record_view_06 TO 'patient_P_2024_06'@'localhost';
GRANT SELECT ON hos.patient_record_view_07 TO 'patient_P_2024_07'@'localhost';
GRANT SELECT ON hos.patient_record_view_08 TO 'patient_P_2024_08'@'localhost';
GRANT SELECT ON hos.patient_record_view_09 TO 'patient_P_2024_09'@'localhost';
GRANT SELECT ON hos.patient_record_view_10 TO 'patient_P_2024_10'@'localhost';
GRANT SELECT ON hos.patient_record_view_11 TO 'patient_P_2024_11'@'localhost';
GRANT SELECT ON hos.patient_record_view_12 TO 'patient_P_2024_12'@'localhost';
GRANT SELECT ON hos.patient_record_view_13 TO 'patient_P_2024_13'@'localhost';
GRANT SELECT ON hos.patient_record_view_14 TO 'patient_P_2024_14'@'localhost';
GRANT SELECT ON hos.patient_record_view_15 TO 'patient_P_2024_15'@'localhost';
```

## 查看patient_record_view結果
```
SELECT *FROM patient_record_view_01;
```
![image](https://github.com/user-attachments/assets/4badeee1-2185-4e0a-b4d1-715f4c9b71ef)

```
SELECT *FROM patient_record_view_02;
```
![image](https://github.com/user-attachments/assets/4b3bfbf0-7eb8-476a-808e-776b548a691b)

```
SELECT *FROM patient_record_view_03;
```
![image](https://github.com/user-attachments/assets/3544d97f-10a8-4f4b-9387-b38330387f0f)

```
SELECT *FROM patient_record_view_04;
```
![image](https://github.com/user-attachments/assets/77092d52-189e-4168-b3b8-e309e5a86828)

```
SELECT *FROM patient_record_view_05;
```
![image](https://github.com/user-attachments/assets/2de3236e-1181-4c3e-b357-ee838f11016e)

```
SELECT *FROM patient_record_view_06;
```
![image](https://github.com/user-attachments/assets/6d0f889c-140e-4430-bf28-526b65714724)

```
SELECT *FROM patient_record_view_07;
```
![image](https://github.com/user-attachments/assets/a7662c72-870c-478c-be41-279c1583da9c)

```
SELECT *FROM patient_record_view_08;
```
![image](https://github.com/user-attachments/assets/f52154b4-92d6-4a51-ba5d-47f78a4af9a8)

```
SELECT *FROM patient_record_view_09;
```
![image](https://github.com/user-attachments/assets/7920bae2-b143-4b02-a32f-731708f60c3e)

```
SELECT *FROM patient_record_view_10;
```
![image](https://github.com/user-attachments/assets/4f0c46ab-5cc2-4ca4-ad4a-89cb9582625c)

```
SELECT *FROM patient_record_view_11;
```
![image](https://github.com/user-attachments/assets/d5939367-959a-4c2e-b048-3cc33e7571a0)

```
SELECT *FROM patient_record_view_12;
```
![image](https://github.com/user-attachments/assets/021343d4-6fc7-4bcc-9916-2eb708e82874)

```
SELECT *FROM patient_record_view_13;
```
![image](https://github.com/user-attachments/assets/86237d3f-4442-4f16-b2f8-1ee33153648d)

```
SELECT *FROM patient_record_view_14;
```
![image](https://github.com/user-attachments/assets/deff3b39-59b3-4cab-ab1c-b46421647f97)

```
SELECT *FROM patient_record_view_15;
```
![image](https://github.com/user-attachments/assets/88fce2ac-8ccd-469c-900d-0a7254eed8c1)


## 查看權限設定是否正確
```
SHOW GRANTS FOR 'patient_P_2024_01'@'localhost';
```
![image](https://github.com/user-attachments/assets/a297a7ef-1089-4290-90ac-306af5f15b31)

```
SHOW GRANTS FOR 'patient_P_2024_02'@'localhost';
```
![image](https://github.com/user-attachments/assets/7f27dda6-f4c0-427c-898f-33b9d81f1ca0)

```
SHOW GRANTS FOR 'patient_P_2024_03'@'localhost';
```
![image](https://github.com/user-attachments/assets/994a9604-4116-4050-adb3-44ab70d3161c)

```
SHOW GRANTS FOR 'patient_P_2024_04'@'localhost';
```
![image](https://github.com/user-attachments/assets/911625b8-85d3-4e20-8e9d-5c2c3137762d)

```
SHOW GRANTS FOR 'patient_P_2024_05'@'localhost';
```
![image](https://github.com/user-attachments/assets/446035ad-f16c-4531-a231-259b716f7c97)

```
SHOW GRANTS FOR 'patient_P_2024_06'@'localhost';
```
![image](https://github.com/user-attachments/assets/4a739aae-ae0b-46ad-bd15-045c5e7982f8)

```
SHOW GRANTS FOR 'patient_P_2024_07'@'localhost';
```
![image](https://github.com/user-attachments/assets/abb39e03-6226-45e5-9f06-f5468421cbcb)

```
SHOW GRANTS FOR 'patient_P_2024_08'@'localhost';
```
![image](https://github.com/user-attachments/assets/cf73157e-3232-4629-bc9d-be857d0517b5)

```
SHOW GRANTS FOR 'patient_P_2024_09'@'localhost';
```
![image](https://github.com/user-attachments/assets/7d294d50-af8a-43cb-98fb-a8d90c567239)

```
SHOW GRANTS FOR 'patient_P_2024_10'@'localhost';
```
![image](https://github.com/user-attachments/assets/2a005147-750e-4580-b2f3-57ac152e02c9)

```
SHOW GRANTS FOR 'patient_P_2024_11'@'localhost';
```
![image](https://github.com/user-attachments/assets/1c3d04f0-9bb3-4270-8dac-0501369e1f22)

```
SHOW GRANTS FOR 'patient_P_2024_12'@'localhost';
```
![image](https://github.com/user-attachments/assets/57c30dd3-da88-496f-bb08-fdb0f0e9bb84)

```
SHOW GRANTS FOR 'patient_P_2024_13'@'localhost';
```
![image](https://github.com/user-attachments/assets/fb131956-b539-4a63-a3f9-f603ca73d1ec)

```
SHOW GRANTS FOR 'patient_P_2024_14'@'localhost';
```
![image](https://github.com/user-attachments/assets/67bc9ff5-31cc-4380-989d-185247187c9f)

```
SHOW GRANTS FOR 'patient_P_2024_15'@'localhost';
```
![image](https://github.com/user-attachments/assets/8451a73f-1a49-43e2-a642-3624d1ab0572)


## 建立醫生查看病患預約情形view

```
CREATE OR REPLACE VIEW doctor_appointments_view_01 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時間,
    s.clinic AS 診間,
    a.number AS 預約號碼,
    a.status AS 預約狀態
FROM appointment a
JOIN patient p ON a.patient_id = p.patient_id
JOIN schedule s ON a.schedule_id = s.schedule_id
JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE d.doctor_id = 'D-001';
```
```
CREATE OR REPLACE VIEW doctor_appointments_view_02 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時間,
    s.clinic AS 診間,
    a.number AS 預約號碼,
    a.status AS 預約狀態
FROM appointment a
JOIN patient p ON a.patient_id = p.patient_id
JOIN schedule s ON a.schedule_id = s.schedule_id
JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE d.doctor_id = 'D-002';
```
```
CREATE OR REPLACE VIEW doctor_appointments_view_03 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時間,
    s.clinic AS 診間,
    a.number AS 預約號碼,
    a.status AS 預約狀態
FROM appointment a
JOIN patient p ON a.patient_id = p.patient_id
JOIN schedule s ON a.schedule_id = s.schedule_id
JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE d.doctor_id = 'D-003';
```
```
CREATE OR REPLACE VIEW doctor_appointments_view_04 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時間,
    s.clinic AS 診間,
    a.number AS 預約號碼,
    a.status AS 預約狀態
FROM appointment a
JOIN patient p ON a.patient_id = p.patient_id
JOIN schedule s ON a.schedule_id = s.schedule_id
JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE d.doctor_id = 'D-004';
```
```
CREATE OR REPLACE VIEW doctor_appointments_view_05 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時間,
    s.clinic AS 診間,
    a.number AS 預約號碼,
    a.status AS 預約狀態
FROM appointment a
JOIN patient p ON a.patient_id = p.patient_id
JOIN schedule s ON a.schedule_id = s.schedule_id
JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE d.doctor_id = 'D-005';
```

```
CREATE OR REPLACE VIEW doctor_appointments_view_06 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時間,
    s.clinic AS 診間,
    a.number AS 預約號碼,
    a.status AS 預約狀態
FROM appointment a
JOIN patient p ON a.patient_id = p.patient_id
JOIN schedule s ON a.schedule_id = s.schedule_id
JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE d.doctor_id = 'D-006';
```
```
CREATE OR REPLACE VIEW doctor_appointments_view_07 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時間,
    s.clinic AS 診間,
    a.number AS 預約號碼,
    a.status AS 預約狀態
FROM appointment a
JOIN patient p ON a.patient_id = p.patient_id
JOIN schedule s ON a.schedule_id = s.schedule_id
JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE d.doctor_id = 'D-007';
```
```
CREATE OR REPLACE VIEW doctor_appointments_view_08 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時間,
    s.clinic AS 診間,
    a.number AS 預約號碼,
    a.status AS 預約狀態
FROM appointment a
JOIN patient p ON a.patient_id = p.patient_id
JOIN schedule s ON a.schedule_id = s.schedule_id
JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE d.doctor_id = 'D-008';
```
```
CREATE OR REPLACE VIEW doctor_appointments_view_09 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時間,
    s.clinic AS 診間,
    a.number AS 預約號碼,
    a.status AS 預約狀態
FROM appointment a
JOIN patient p ON a.patient_id = p.patient_id
JOIN schedule s ON a.schedule_id = s.schedule_id
JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE d.doctor_id = 'D-009';
```
```
CREATE OR REPLACE VIEW doctor_appointments_view_10 AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時間,
    s.clinic AS 診間,
    a.number AS 預約號碼,
    a.status AS 預約狀態
FROM appointment a
JOIN patient p ON a.patient_id = p.patient_id
JOIN schedule s ON a.schedule_id = s.schedule_id
JOIN doctor d ON s.doctor_id = d.doctor_id
WHERE d.doctor_id = 'D-010';
```
## 建立醫生使用者
```
CREATE USER 'doctor_D-001'@'localhost' IDENTIFIED BY 'D-001';
CREATE USER 'doctor_D-002'@'localhost' IDENTIFIED BY 'D-002';
CREATE USER 'doctor_D-003'@'localhost' IDENTIFIED BY 'D-003';
CREATE USER 'doctor_D-004'@'localhost' IDENTIFIED BY 'D-004';
CREATE USER 'doctor_D-005'@'localhost' IDENTIFIED BY 'D-005';
CREATE USER 'doctor_D-006'@'localhost' IDENTIFIED BY 'D-006';
CREATE USER 'doctor_D-007'@'localhost' IDENTIFIED BY 'D-007';
CREATE USER 'doctor_D-008'@'localhost' IDENTIFIED BY 'D-008';
CREATE USER 'doctor_D-009'@'localhost' IDENTIFIED BY 'D-009';
CREATE USER 'doctor_D-010'@'localhost' IDENTIFIED BY 'D-010';

```

## 設定doctor_appointments_view權限
```
GRANT SELECT ON hos.doctor_appointments_view_01 TO 'doctor_D-001'@'localhost';
GRANT SELECT ON hos.doctor_appointments_view_02 TO 'doctor_D-002'@'localhost';
GRANT SELECT ON hos.doctor_appointments_view_03 TO 'doctor_D-003'@'localhost';
GRANT SELECT ON hos.doctor_appointments_view_04 TO 'doctor_D-004'@'localhost';
GRANT SELECT ON hos.doctor_appointments_view_05 TO 'doctor_D-005'@'localhost';
GRANT SELECT ON hos.doctor_appointments_view_06 TO 'doctor_D-006'@'localhost';
GRANT SELECT ON hos.doctor_appointments_view_07 TO 'doctor_D-007'@'localhost';
GRANT SELECT ON hos.doctor_appointments_view_08 TO 'doctor_D-008'@'localhost';
GRANT SELECT ON hos.doctor_appointments_view_09 TO 'doctor_D-009'@'localhost';
GRANT SELECT ON hos.doctor_appointments_view_10 TO 'doctor_D-010'@'localhost';
```

## 查看doctor_appointments_view結果
```
SELECT *FROM doctor_appointments_view_01;
```
![image](https://github.com/user-attachments/assets/acfeff90-d069-4495-ac43-529f8b8f0877)

```
SELECT *FROM doctor_appointments_view_02;
```
![image](https://github.com/user-attachments/assets/09cfd74b-7445-4e84-8129-e8f2c0dae9d0)

```
SELECT *FROM doctor_appointments_view_03;
```
![image](https://github.com/user-attachments/assets/18ad55f1-1e63-4a2e-ae72-c98e16e7a0c6)

```
SELECT *FROM doctor_appointments_view_04;
```
![image](https://github.com/user-attachments/assets/b9d6fe59-e896-4400-91b2-0e5ff193c4a9)

```
SELECT *FROM doctor_appointments_view_05;
```
![image](https://github.com/user-attachments/assets/a0c7281d-b789-4792-9972-1d333f3e2328)

```
SELECT *FROM doctor_appointments_view_06;
```
![image](https://github.com/user-attachments/assets/e23d455a-c227-45b2-b979-2762662431d7)

```
SELECT *FROM doctor_appointments_view_07;
```
![image](https://github.com/user-attachments/assets/90fafa58-3d67-4447-81ac-4795e2c38039)

```
SELECT *FROM doctor_appointments_view_08;
```
![image](https://github.com/user-attachments/assets/df4eea70-7023-4f38-83cc-862994417ce4)

```
SELECT *FROM doctor_appointments_view_09;
```
![image](https://github.com/user-attachments/assets/5febab2e-8cf9-494c-9749-9a4f9b0ae265)

```
SELECT *FROM doctor_appointments_view_10;
```
![image](https://github.com/user-attachments/assets/9175c916-c9db-4185-92a6-82416752be3d)




## 創建醫生查看班表view
```
CREATE OR REPLACE VIEW doctor_schedule_view_01 AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    s.schedule_id AS 排班編號,
    s.schedule_date AS 排班日期,
    s.schedule_time AS 排班時段,
    s.week AS 星期,
    s.clinic AS 診間,
    s.schedule_status AS 狀態
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
WHERE d.doctor_id = 'D-001';

```
```
CREATE OR REPLACE VIEW doctor_schedule_view_02 AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    s.schedule_id AS 排班編號,
    s.schedule_date AS 排班日期,
    s.schedule_time AS 排班時段,
    s.week AS 星期,
    s.clinic AS 診間,
    s.schedule_status AS 狀態
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
WHERE d.doctor_id = 'D-002';

```
```
CREATE OR REPLACE VIEW doctor_schedule_view_03 AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    s.schedule_id AS 排班編號,
    s.schedule_date AS 排班日期,
    s.schedule_time AS 排班時段,
    s.week AS 星期,
    s.clinic AS 診間,
    s.schedule_status AS 狀態
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
WHERE d.doctor_id = 'D-003';

```
```
CREATE OR REPLACE VIEW doctor_schedule_view_04 AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    s.schedule_id AS 排班編號,
    s.schedule_date AS 排班日期,
    s.schedule_time AS 排班時段,
    s.week AS 星期,
    s.clinic AS 診間,
    s.schedule_status AS 狀態
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
WHERE d.doctor_id = 'D-004';

```

```
CREATE OR REPLACE VIEW doctor_schedule_view_05 AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    s.schedule_id AS 排班編號,
    s.schedule_date AS 排班日期,
    s.schedule_time AS 排班時段,
    s.week AS 星期,
    s.clinic AS 診間,
    s.schedule_status AS 狀態
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
WHERE d.doctor_id = 'D-005';

```
```
CREATE OR REPLACE VIEW doctor_schedule_view_06 AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    s.schedule_id AS 排班編號,
    s.schedule_date AS 排班日期,
    s.schedule_time AS 排班時段,
    s.week AS 星期,
    s.clinic AS 診間,
    s.schedule_status AS 狀態
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
WHERE d.doctor_id = 'D-006';

```
```
CREATE OR REPLACE VIEW doctor_schedule_view_07 AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    s.schedule_id AS 排班編號,
    s.schedule_date AS 排班日期,
    s.schedule_time AS 排班時段,
    s.week AS 星期,
    s.clinic AS 診間,
    s.schedule_status AS 狀態
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
WHERE d.doctor_id = 'D-007';

```
```
CREATE OR REPLACE VIEW doctor_schedule_view_08 AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    s.schedule_id AS 排班編號,
    s.schedule_date AS 排班日期,
    s.schedule_time AS 排班時段,
    s.week AS 星期,
    s.clinic AS 診間,
    s.schedule_status AS 狀態
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
WHERE d.doctor_id = 'D-008';

```
```
CREATE OR REPLACE VIEW doctor_schedule_view_09 AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    s.schedule_id AS 排班編號,
    s.schedule_date AS 排班日期,
    s.schedule_time AS 排班時段,
    s.week AS 星期,
    s.clinic AS 診間,
    s.schedule_status AS 狀態
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
WHERE d.doctor_id = 'D-009';

```

```
CREATE OR REPLACE VIEW doctor_schedule_view_10 AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    s.schedule_id AS 排班編號,
    s.schedule_date AS 排班日期,
    s.schedule_time AS 排班時段,
    s.week AS 星期,
    s.clinic AS 診間,
    s.schedule_status AS 狀態
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
WHERE d.doctor_id = 'D-010';

```

## 設定doctor_schedule_view權限
```
GRANT SELECT ON hos.doctor_schedule_view_01 TO 'doctor_D-001'@'localhost';
GRANT SELECT ON hos.doctor_schedule_view_02 TO 'doctor_D-002'@'localhost';
GRANT SELECT ON hos.doctor_schedule_view_03 TO 'doctor_D-003'@'localhost';
GRANT SELECT ON hos.doctor_schedule_view_04 TO 'doctor_D-004'@'localhost';
GRANT SELECT ON hos.doctor_schedule_view_05 TO 'doctor_D-005'@'localhost';
GRANT SELECT ON hos.doctor_schedule_view_06 TO 'doctor_D-006'@'localhost';
GRANT SELECT ON hos.doctor_schedule_view_07 TO 'doctor_D-007'@'localhost';
GRANT SELECT ON hos.doctor_schedule_view_08 TO 'doctor_D-008'@'localhost';
GRANT SELECT ON hos.doctor_schedule_view_09 TO 'doctor_D-009'@'localhost';
GRANT SELECT ON hos.doctor_schedule_view_10 TO 'doctor_D-010'@'localhost';

```

## 查看doctor_schedule_view結果
```
SELECT *FROM doctor_schedule_view_01;
```
![image](https://github.com/user-attachments/assets/06402690-c107-4635-85c5-788119d4199e)

```
SELECT *FROM doctor_schedule_view_02;
```
![image](https://github.com/user-attachments/assets/197cf4b1-c55c-4d22-a94d-9b63b7cfcb09)

```
SELECT *FROM doctor_schedule_view_03;
```
![image](https://github.com/user-attachments/assets/b8ce3cef-a2ac-4aa5-abee-b566cce97231)

```
SELECT *FROM doctor_schedule_view_04;
```
![image](https://github.com/user-attachments/assets/ce8bd2e6-50b4-41bd-bab3-5806d69400c9)

```
SELECT *FROM doctor_schedule_view_05;
```
![image](https://github.com/user-attachments/assets/9c6911dd-3e85-4786-af2a-e744b31bdb6e)

```
SELECT *FROM doctor_schedule_view_06;
```
![image](https://github.com/user-attachments/assets/745e3bc9-4a2a-4959-984b-9c4fb7e920c5)

```
SELECT *FROM doctor_schedule_view_07;
```
![image](https://github.com/user-attachments/assets/d84e39b8-17f5-4ec2-894b-875781be45f4)

```
SELECT *FROM doctor_schedule_view_08;
```
![image](https://github.com/user-attachments/assets/a98d0af5-3a9a-4720-ab3b-dd3254ce13ab)

```
SELECT *FROM doctor_schedule_view_09;
```
![image](https://github.com/user-attachments/assets/c3cf9923-2bf3-4756-a0ba-f1a37ec19067)

```
SELECT *FROM doctor_schedule_view_10;
```
![image](https://github.com/user-attachments/assets/27a6f121-70f8-4b35-a41d-0069910bbae9)



## 創建醫生查看病例view
```
CREATE OR REPLACE VIEW doctor_medical_record_view_01 AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    mr.medical_record_id AS 病歷編號,
    mr.diagnosis_record AS 診斷紀錄,
    mr.visits_date AS 看診日期
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
JOIN appointment a ON s.schedule_id = a.schedule_id
JOIN medical_record mr ON a.medical_record_id = mr.medical_record_id
JOIN patient p ON a.patient_id = p.patient_id
WHERE d.doctor_id = 'D-001';

```
```
CREATE OR REPLACE VIEW doctor_medical_record_view_02 AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    mr.medical_record_id AS 病歷編號,
    mr.diagnosis_record AS 診斷紀錄,
    mr.visits_date AS 看診日期
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
JOIN appointment a ON s.schedule_id = a.schedule_id
JOIN medical_record mr ON a.medical_record_id = mr.medical_record_id
JOIN patient p ON a.patient_id = p.patient_id
WHERE d.doctor_id = 'D-002';

```
```
CREATE OR REPLACE VIEW doctor_medical_record_view_03 AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    mr.medical_record_id AS 病歷編號,
    mr.diagnosis_record AS 診斷紀錄,
    mr.visits_date AS 看診日期
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
JOIN appointment a ON s.schedule_id = a.schedule_id
JOIN medical_record mr ON a.medical_record_id = mr.medical_record_id
JOIN patient p ON a.patient_id = p.patient_id
WHERE d.doctor_id = 'D-003';

```
```
CREATE OR REPLACE VIEW doctor_medical_record_view_04 AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    mr.medical_record_id AS 病歷編號,
    mr.diagnosis_record AS 診斷紀錄,
    mr.visits_date AS 看診日期
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
JOIN appointment a ON s.schedule_id = a.schedule_id
JOIN medical_record mr ON a.medical_record_id = mr.medical_record_id
JOIN patient p ON a.patient_id = p.patient_id
WHERE d.doctor_id = 'D-004';

```
```
CREATE OR REPLACE VIEW doctor_medical_record_view_05 AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    mr.medical_record_id AS 病歷編號,
    mr.diagnosis_record AS 診斷紀錄,
    mr.visits_date AS 看診日期
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
JOIN appointment a ON s.schedule_id = a.schedule_id
JOIN medical_record mr ON a.medical_record_id = mr.medical_record_id
JOIN patient p ON a.patient_id = p.patient_id
WHERE d.doctor_id = 'D-005';

```
```
CREATE OR REPLACE VIEW doctor_medical_record_view_06 AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    mr.medical_record_id AS 病歷編號,
    mr.diagnosis_record AS 診斷紀錄,
    mr.visits_date AS 看診日期
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
JOIN appointment a ON s.schedule_id = a.schedule_id
JOIN medical_record mr ON a.medical_record_id = mr.medical_record_id
JOIN patient p ON a.patient_id = p.patient_id
WHERE d.doctor_id = 'D-006';

```
```
CREATE OR REPLACE VIEW doctor_medical_record_view_07 AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    mr.medical_record_id AS 病歷編號,
    mr.diagnosis_record AS 診斷紀錄,
    mr.visits_date AS 看診日期
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
JOIN appointment a ON s.schedule_id = a.schedule_id
JOIN medical_record mr ON a.medical_record_id = mr.medical_record_id
JOIN patient p ON a.patient_id = p.patient_id
WHERE d.doctor_id = 'D-007';

```
```
CREATE OR REPLACE VIEW doctor_medical_record_view_08 AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    mr.medical_record_id AS 病歷編號,
    mr.diagnosis_record AS 診斷紀錄,
    mr.visits_date AS 看診日期
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
JOIN appointment a ON s.schedule_id = a.schedule_id
JOIN medical_record mr ON a.medical_record_id = mr.medical_record_id
JOIN patient p ON a.patient_id = p.patient_id
WHERE d.doctor_id = 'D-008';

```
```
CREATE OR REPLACE VIEW doctor_medical_record_view_09 AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    mr.medical_record_id AS 病歷編號,
    mr.diagnosis_record AS 診斷紀錄,
    mr.visits_date AS 看診日期
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
JOIN appointment a ON s.schedule_id = a.schedule_id
JOIN medical_record mr ON a.medical_record_id = mr.medical_record_id
JOIN patient p ON a.patient_id = p.patient_id
WHERE d.doctor_id = 'D-009';

```
```
CREATE OR REPLACE VIEW doctor_medical_record_view_10 AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    mr.medical_record_id AS 病歷編號,
    mr.diagnosis_record AS 診斷紀錄,
    mr.visits_date AS 看診日期
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
JOIN appointment a ON s.schedule_id = a.schedule_id
JOIN medical_record mr ON a.medical_record_id = mr.medical_record_id
JOIN patient p ON a.patient_id = p.patient_id
WHERE d.doctor_id = 'D-010';

```
## 設定doctor_medical_record_view權限
```
GRANT SELECT ON hos.doctor_medical_record_view_01 TO 'doctor_D-001'@'localhost';
GRANT SELECT ON hos.doctor_medical_record_view_02 TO 'doctor_D-002'@'localhost';
GRANT SELECT ON hos.doctor_medical_record_view_03 TO 'doctor_D-003'@'localhost';
GRANT SELECT ON hos.doctor_medical_record_view_04 TO 'doctor_D-004'@'localhost';
GRANT SELECT ON hos.doctor_medical_record_view_05 TO 'doctor_D-005'@'localhost';
GRANT SELECT ON hos.doctor_medical_record_view_06 TO 'doctor_D-006'@'localhost';
GRANT SELECT ON hos.doctor_medical_record_view_07 TO 'doctor_D-007'@'localhost';
GRANT SELECT ON hos.doctor_medical_record_view_08 TO 'doctor_D-008'@'localhost';
GRANT SELECT ON hos.doctor_medical_record_view_09 TO 'doctor_D-009'@'localhost';
GRANT SELECT ON hos.doctor_medical_record_view_10 TO 'doctor_D-010'@'localhost';
```

## 查看doctor_medical_record_view結果
```
SELECT *FROM doctor_medical_record_view_01;
```
![image](https://github.com/user-attachments/assets/ad15a80c-e67e-41a6-acd1-a82785f86f2f)

```
SELECT *FROM doctor_medical_record_view_02;
```
![image](https://github.com/user-attachments/assets/3b84c214-65f8-4f2b-bf64-25b8e7084af0)

```
SELECT *FROM doctor_medical_record_view_03;
```
![image](https://github.com/user-attachments/assets/4f7727f1-4f5d-4f58-a355-771c5e99b0e9)

```
SELECT *FROM doctor_medical_record_view_04;
```
![image](https://github.com/user-attachments/assets/eb12ba1e-b61e-46f5-96e3-9b18ad9c2e54)

```
SELECT *FROM doctor_medical_record_view_05;
```
![image](https://github.com/user-attachments/assets/c1623976-6105-4145-98b8-1c97aa81c6d6)

```
SELECT *FROM doctor_medical_record_view_06;
```
![image](https://github.com/user-attachments/assets/0123b66a-befd-4b58-becf-3c43ced653ae)

```
SELECT *FROM doctor_medical_record_view_07;
```
![image](https://github.com/user-attachments/assets/8207bfef-a59f-4673-9c1a-d4648f450957)

```
SELECT *FROM doctor_medical_record_view_08;
```
![image](https://github.com/user-attachments/assets/682b96e1-7432-4af6-a0cb-8366bbd14e29)

```
SELECT *FROM doctor_medical_record_view_09;
```
![image](https://github.com/user-attachments/assets/f2b2d96b-c14e-4098-a3da-49aeb997e59c)

```
SELECT *FROM doctor_medical_record_view_10;
```
![image](https://github.com/user-attachments/assets/36066047-6768-4094-967f-479b161918c7)


## 確認權限是否設定正確
```
SHOW GRANTS FOR 'doctor_D-001'@'localhost';
```
![image](https://github.com/user-attachments/assets/47addb5f-6bc5-48be-8486-f18983299041)

```
SHOW GRANTS FOR 'doctor_D-002'@'localhost';
```
![image](https://github.com/user-attachments/assets/30f74959-96e7-469d-b39a-6de119f152b0)

```
SHOW GRANTS FOR 'doctor_D-003'@'localhost';
```
![image](https://github.com/user-attachments/assets/d52196dc-8110-410e-be4e-a407114954e8)

```
SHOW GRANTS FOR 'doctor_D-004'@'localhost';
```
![image](https://github.com/user-attachments/assets/5bb5996b-3c8c-4816-ac3b-ba66f151144a)

```
SHOW GRANTS FOR 'doctor_D-005'@'localhost';
```
![image](https://github.com/user-attachments/assets/456de609-d39b-4c80-934e-64fd41c2fb97)

```
SHOW GRANTS FOR 'doctor_D-006'@'localhost';
```
![image](https://github.com/user-attachments/assets/6bebac60-34ba-4467-b430-5785a054acd2)

```
SHOW GRANTS FOR 'doctor_D-007'@'localhost';
```
![image](https://github.com/user-attachments/assets/583b449d-0fb8-4c1e-a1d9-fb493e49f2de)

```
SHOW GRANTS FOR 'doctor_D-008'@'localhost';
```
![image](https://github.com/user-attachments/assets/023b5293-1eb4-4a61-9c85-8632daf61d70)

```
SHOW GRANTS FOR 'doctor_D-009'@'localhost';
```
![image](https://github.com/user-attachments/assets/2597938e-ab58-4a52-adf5-59f38cfa5a7c)

```
SHOW GRANTS FOR 'doctor_D-010'@'localhost';
```
![image](https://github.com/user-attachments/assets/d9da4795-7f11-45d6-a795-241cadd3fdc3)



## 建立管理員查看醫生與病患的預約資料view
```
CREATE OR REPLACE VIEW doctor_patient_detail_view AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    p.gender AS 病人性別,
    p.birth_date AS 出生日期,
    p.phone AS 病人電話,
    mr.medical_record_id AS 病歷編號,
    mr.diagnosis_record AS 診斷紀錄,
    mr.visits_date AS 就診日期,
    a.appointment_id AS 預約編號,
    a.status AS 預約狀態,
    s.schedule_date AS 預約日期,
    s.schedule_time AS 預約時間,
    s.clinic AS 診間
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
JOIN appointment a ON s.schedule_id = a.schedule_id
JOIN patient p ON a.patient_id = p.patient_id
LEFT JOIN medical_record mr ON a.medical_record_id = mr.medical_record_id;

```

<img width="904" alt="image" src="https://github.com/user-attachments/assets/3e134640-76c9-4160-99e3-469a0799efc4" />


## 建立管理員查看整體病歷view
```
CREATE OR REPLACE VIEW doctor_patient_medical_records_view AS
SELECT
    d.doctor_id AS 醫生編號,
    d.name AS 醫生姓名,
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    mr.medical_record_id AS 病歷編號,
    mr.diagnosis_record AS 診斷紀錄,
    mr.visits_date AS 就診日期
FROM doctor d
JOIN schedule s ON d.doctor_id = s.doctor_id
JOIN appointment a ON s.schedule_id = a.schedule_id
JOIN patient p ON a.patient_id = p.patient_id
JOIN medical_record mr ON a.medical_record_id = mr.medical_record_id
ORDER BY p.patient_id, mr.visits_date DESC;
```
<img width="695" alt="image" src="https://github.com/user-attachments/assets/9108faee-29a6-4731-bbd7-306c44320d0d" />




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



