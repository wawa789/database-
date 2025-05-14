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

![image](https://github.com/user-attachments/assets/fa8a0542-79df-4943-b29f-716f2ec601e0)


## doctors 表（醫生資料表）

![image](https://github.com/user-attachments/assets/0fd0334d-8328-4e09-af90-221589aa909b)


## appointments表（預約資料表）

![image](https://github.com/user-attachments/assets/3969f3fc-2608-42e9-961d-e4e4a71d5994)


## medical_record表（病歷資料表）

![image](https://github.com/user-attachments/assets/14c9b878-ac34-4d7c-89ba-f6b81cd767a9)



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

## 新增病患資料
```
INSERT INTO patient (name, phone, birth_date, gender, national_id, resident_id) VALUES
('王小明', '0912345678', '1990-01-15', 'M', 'A123456789', NULL),
('李美麗', '0922333444', '1985-06-28', 'F', 'B223456789', NULL),
('陳建宏', '0933221144', '1975-12-02', 'M', 'C123456789', NULL),
('黃凱婷', '0955667788', '1992-04-10', 'F', NULL, 'A800000001'),
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


## 簡報
https://www.canva.com/design/DAGj82tfSmY/Q-CFpZqbAzo32BPzIDAeGA/edit
