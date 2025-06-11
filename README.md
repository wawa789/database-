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
CREATE TABLE medical_record (
    medical_record_id VARCHAR(30) PRIMARY KEY,
    patient_id VARCHAR(30),
    diagnosis_record TEXT,
    last_visits_date DATE,
    FOREIGN KEY (patient_id) REFERENCES patient(patient_id)
);
```

## 預約表
```
CREATE TABLE appointment (
    appointment_id VARCHAR(30) PRIMARY KEY,
    patient_id VARCHAR(30),
    doctor_id VARCHAR(30),
    status TEXT,
    appointment_time TEXT,
    medical_record_id VARCHAR(30),
    clinic VARCHAR(10),
    number VARCHAR(10),
    FOREIGN KEY (medical_record_id) REFERENCES medical_record(medical_record_id),
    FOREIGN KEY (doctor_id) REFERENCES doctor(doctor_id)
);
```

## 醫生排班表
```
CREATE TABLE schedule (
    schedule_id INTEGER PRIMARY KEY,
    doctor_id VARCHAR(30),
    schedule_date DATE,
    schedule_time TEXT,
    week TEXT,
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
('P-2023-13', 'F165045923', '柯峻鋒', '男', '1999-09-28', '0939002124'),
('P-2023-14', 'H147258175', '蘇耀元', '男', '1980-03-22', '0917783213'),
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
INSERT INTO medical_record (medical_record_id, patient_id, diagnosis_record, last_visits_date) VALUES
(1, 'P-2024-01', '蛀牙', '2024-08-07'),
(2, 'P-2024-02', '牙周病', '2024-04-21'),
(3, 'P-2024-03', '智齒拔除', '2024-09-04'),
(4, 'P-2024-04', '牙齒美白', '2024-03-27'),
(5, 'P-2024-05', '洗牙', '2023-11-19'),
(6, 'P-2024-06', '牙齒矯正', '2024-02-14'),
(7, 'P-2024-07', '補牙', '2024-03-13'),
(8, 'P-2023-08', '牙齦炎', '2023-09-17'),
(9, 'P-2023-09', '牙齒裂痕', '2024-07-15'),
(10, 'P-2024-10', '牙冠製作', '2023-01-13'),
(11, 'P-2024-11','洗牙', '1975-10-21'),
(12, 'P-2024-12', '牙齒矯正', '2000-09-21'),
(13, 'P-2023-13', '智齒拔除', '1999-09-28'),
(14, 'P-2023-14', '牙齦炎', '1980-03-22'),
(15, 'P-2024-15', '洗牙', '1995-10-10');
```

## 新增醫生排班資料

```
INSERT INTO schedule (schedule_id, doctor_id, schedule_date, schedule_time, week, schedule_status) VALUES
(1, 'D-001', '2025-05-21', '上午', '星期一', '已滿'),
(2, 'D-002', '2025-05-22', '上午', '星期二', '開診'),
(3, 'D-003', '2025-05-23', '上午', '星期三', '開診'),
(4, 'D-004', '2025-05-24', '下午', '星期四', '休診'),
(5, 'D-005', '2025-05-25', '下午', '星期五', '開診'),
(6, 'D-006', '2025-05-26', '下午', '星期一', '開診'),
(7, 'D-007', '2025-05-27', '下午', '星期二', '開診'),
(8, 'D-008', '2025-05-28', '晚上', '星期三', '休診'),
(9, 'D-009', '2025-05-29', '晚上', '星期四', '開診'),
(10, 'D-010', '2025-05-30', '晚上', '星期五', '開診');
```

## 新增預約表資料
```
INSERT INTO appointment (appointment_id, patient_id, doctor_id, status, appointment_time, clinic, number) VALUES
('2025-04-21-001', 'P-2024-01', 'D-001', '已預約', '2025-05-21 09:00','101診間','1號'),
('2025-04-22-002', 'P-2024-02', 'D-002', '已完成', '2025-05-22 10:00','101診間','NULL'),
('2025-04-23-003', 'P-2024-03', 'D-003', '取消', '2025-05-23 11:00','101診間','NULL'),
('2025-04-24-004', 'P-2024-04', 'D-004', '已預約', '2025-05-24 14:00','102診間','1號'),
('2025-04-25-005', 'P-2024-05', 'D-005', '已預約', '2025-05-25 13:00','102診間','1號'),
('2025-04-26-006', 'P-2024-06', 'D-006', '已完成', '2025-05-26 15:00','103診間','NULL'),
('2025-04-27-007', 'P-2024-07', 'D-007', '已預約', '2025-05-27 10:00','103診間','1號'),
('2025-04-28-008', 'P-2024-08', 'D-008', '取消', '2025-05-28 16:00','103診間','NULL'),
('2025-04-29-009', 'P-2024-09', 'D-009', '已完成', '2025-05-29 11:00','104診間','NULL'),
('2025-04-30-010', 'P-2024-10','D-010', '已預約', '2025-05-21 09:00','104診間','1號'),
('2025-05-01-011', 'P-2024-11', 'D-001', '已完成', '2025-05-21 09:30','101診間','2號'),
('2025-05-02-012', 'P-2024-12', 'D-001', '已預約', '2025-05-21 10:00','101診間','3號'),
('2025-05-03-013', 'P-2024-13', 'D-004', '取消', '2025-05-24 15:00','102診間','NULL'),
('2025-05-04-014', 'P-2024-14', 'D-002', '已預約', '2025-05-22 11:00','101診間','1號'),
('2025-05-05-015', 'P-2024-15','D-010', '已預約', '2025-05-21 10:30','104診間','2號');
```




## 建立檢視表為醫生可以看到的資訊
```


CREATE OR REPLACE VIEW view_doctor_appointments AS
SELECT 
    d.doctor_id AS 醫師編號,
    d.name AS 醫師姓名,
    p.name AS 病人姓名,
    p.phone AS 病人電話,
    a.status AS 預約狀態,
    a.appointment_time AS 預約時間,
    mr.diagnosis_record AS 診斷紀錄,
    mr.last_visits_date AS 最近就診日期
FROM 
    doctor d
JOIN 
    appointment a ON d.doctor_id = a.doctor_id
JOIN 
    medical_record mr ON a.medical_record_id = mr.medical_record_id
JOIN 
    patient p ON mr.patient_id = p.patient_id;


```


## 建立檢視表為病患可以看到的資訊
```


CREATE OR REPLACE VIEW view_patient_appointments AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    d.name AS 醫師姓名,
    d.specialty AS 專科,
    a.status AS 預約狀態,
    a.appointment_time AS 預約時間,
    mr.diagnosis_record AS 診斷紀錄,
    mr.last_visits_date AS 最近就診日期
FROM 
    patient p
JOIN 
    medical_record mr ON p.patient_id = mr.patient_id
JOIN 
    appointment a ON mr.medical_record_id = a.medical_record_id
JOIN 
    doctor d ON a.doctor_id = d.doctor_id;

```
# 病患查看醫生排班
```CREATE OR REPLACE VIEW view_schedule AS
SELECT
    s.schedule_date AS 日期,
    s.week AS 星期,
    s.schedule_time AS 時段,
    d.name AS 醫師姓名,
    d.specialty AS 專科,
    s.schedule_status AS 狀態
FROM 
    schedule s
JOIN 
    doctor d ON s.doctor_id = d.doctor_id;
```
# 授權 病患
```
GRANT SELECT,INSERT, UPDATE ON patient TO Patient_Account;
GRANT INSERT, UPDATE  (appointment_time,appointment_status) ON appointment  TO Patient_Account ;
GRANT SELECT ON view_patient_appointment TO Patient_Account ;
GRANT SELECT ON view_schedule TO Patient_Account ;
```
# 醫生查看歷史病歷
```
CREATE OR REPLACE VIEW view_doctor_medical_record AS
SELECT 
    p.patient_id AS 病人編號,
    p.name AS 病人姓名,
    mr.medical_record_id AS 病歷編號,
    mr.diagnosis_record AS 就診紀錄,
    mr.last_visits_date AS 就診日期
FROM 
    patient p
JOIN 
    medical_record mr ON p.patient_id = mr.patient_id;
ORDER BY 
    a.appointment_time DESC;
```
# 醫生查看排班
```
CREATE OR REPLACE VIEW view_schedule AS
SELECT
    s.schedule_date AS 日期,
    s.week AS 星期,
    s.schedule_time AS 時段,
    d.name AS 醫師姓名,
    d.specialty AS 專科,
    s.schedule_status AS 狀態
FROM 
    schedule s
JOIN 
    doctor d ON s.doctor_id = d.doctor_id;
```
# 授權
# 醫生
```
GRANT SELECT,INSERT, UPDATE ON medical_record TO Doctor_Account;
GRANT SELECT ON view_doctor_appointment TO Doctor_Account ;
GRANT SELECT ON view_schedule TO Doctor_Account ;
```
# 管理者
```
GRANT ALL PRIVILEGES ON clinic_db.* TO Admin_Account;
```

## 儲存密碼資料庫
## 創建儲存密碼資料表
```
CREATE TABLE auth_db.patients (
    patient_id VARCHAR(30) PRIMARY KEY,
    name VARCHAR(10) NOT NULL,
    ssid VARCHAR(10) NOT NULL,
    password VARCHAR(10) NOT NULL,
FOREIGN KEY (patient_id) REFERENCES hw3.patient(patient_id)
);
```
## 建立每個病患密碼
```
INSERT INTO auth_db.patients (patient_id, name, ssid , password) VALUES
('P-2024-01', '陳玉華', '19701024',  'A225190428'),
('P-2024-02', '黃志明', '19851225',  'B109235501'),
('P-2024-03', '林淑芬', '19860222',  'C274705806'),
('P-2024-04', '張文龍', '19750411',  'D117815766'),
('P-2024-05', '李玉美', '19550714',  'E253941742'),
('P-2024-06', '王志誠', '19951114',  'F110994720'),
('P-2024-07', '吳佩珊', '20180721',  'G231160530'),
('P-2023-08', '趙信宏', '19830824',  'H131347152'),
('P-2023-09', '劉文昌', '19881209', 'I148658852'),
('P-2024-10', '葉秋萍', '19851008', 'J260542851'),
('P-2024-11', '田可名', '19751021', 'J102662605'),
('P-2024-12', '孫泳宜', '20000921', 'E269884203'),
('P-2023-13', '柯峻鋒', '19990928', 'F165045923'),
('P-2023-14', '蘇耀元', '19800322', 'H147258175'),
('P-2024-15', '簡以心', '19951010', 'C205110417');
```

## 每個病患可以看見自己的預約結果(這邊以陳玉華病患作為範例)
```
SELECT
    a.appointment_id,
    a.appointment_time,
    a.status AS appointment_status,
    a.clinic AS appointment_clinic,
    a.number AS appointment_number,
    d.name AS doctor_name,
    d.specialty AS doctor_specialty
FROM
    hw3.appointment AS a
JOIN
    hw3.doctor AS d ON a.doctor_id = d.doctor_id
JOIN
    auth_db.patients AS u ON a.patient_id = u.patient_id
WHERE
    u.ssid = '19701024' AND u.password = 'A225190428';
```

## 建立每個醫生密碼
```
CREATE TABLE auth_db.doctors (
    doctor_id VARCHAR(30) PRIMARY KEY,
    name VARCHAR(10) NOT NULL,
    ssid VARCHAR(10) NOT NULL,
    password VARCHAR(10) NOT NULL,
FOREIGN KEY (doctor_id) REFERENCES hw3.doctor(doctor_id)
);
```
## 建立每個醫生密碼
```
INSERT INTO auth_db.doctors (doctor_id, name, ssid , password) VALUES
('D-001', '王大明', 'D001', '0932716195'),
('D-002', '李小美', 'D002', '0910775159'),
('D-003', '陳志強', 'D003', '0984593191'),
('D-004', '林慧君', 'D004', '0968202494'),
('D-005', '張建宏', 'D005', '0911858069'),
('D-006', '吳佩琪', 'D006', '0961519171'),
('D-007', '周俊豪', 'D007', '0977834772'),
('D-008', '鄭雅芳', 'D008', '0970379877'),
('D-009', '何文豪', 'D009', '0980671879'),
('D-010', '劉曉婷', 'D010', '0968500959');
```

## 每個醫生可以看見病人預約自己的結果(這邊以王大明醫生作為範例)
```
SELECT
    a.appointment_id,
    a.appointment_time,
    a.status AS appointment_status,
    a.clinic AS appointment_clinic,
    a.number AS appointment_number,
    d.name AS doctor_name,
    d.doctor_id,
    d.specialty AS doctor_specialty
FROM
    hw3.appointment AS a
JOIN
    hw3.doctor AS d ON a.doctor_id = d.doctor_id
JOIN
    auth_db.patients AS u ON a.patient_id = u.patient_id
JOIN
    auth_db.doctors AS do ON d.doctor_id = do.doctor_id
WHERE
    do.ssid = 'D001' AND do.password = '0932716195';
```

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
