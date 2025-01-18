# Base de datos

__addresses__

- address_id **PK (UUID)**
- address_file **Optional Varchar(250)**
- address_province **(Varchar 75)**
- address_canton **(Varchar 75)**
- address_parish **(Varchar 75)**
- address_main_street **(Varchar 150)**
- address_secondary _street **(Varchar 200)**
- address_house_number **(Varchar 75)**

__roles__
* role_id **PK (UUID)**
* role_type **String(250) (User, Admin, Technician)**

__Documentations__
* doc_id **PK (UUID)**
* doc_type **String(250) (Identification, Passport)**

__clients__
* client_id **PK (UUID)**
* client_name **Varchar (255)**
* client_email **Varchar (75)**
* client_credentials **FK (doc_id)**
* client_password **Varchar (25)**
* client_rol _*FK (role_id)*_

<!-- Users -->
* client_phone **Varchar (15)**
* client_address _*Fk (adress_id)*_
* client_meters _*Fk (meters_id)*_

* client_isactive **Bool**

* created_at **DateTime**
* updated_at **DateTime**


__water_meters__
* meter_id **PK (UUID)**
* meter_serial_number **Varchar(250)**
* meter_installation **DATETIME**
* meter_type **Varchar(50) (Mechanical, Digital, Ultrasonic)**
* meter_status **Enum (Active, Inactive, Maintenance)**


__meter_readings__
* reading_id **PK (UUID)**
* meter_id **FK (UUID)**
* reading_date **DATETIME**
* consumption **FLOAT**
* recorded_by **FK (UUID)**


__bills__
* bill_id **PK (UUID)**
* client_id **FK (UUID)**
* meter_id **FK (UUID)**
* initial_period **DATE**
* final_period **DATE**
* total_usage **FLOAT**
* total_cost **DECIMAL(10,2)**
* status **Enum (Pending, Paid, Overdue)**


__payments__
* payment_id **PK (UUID)**
* bill_id **FK (UUID)**
* client_id **FK (UUID)**
* amount **DECIMAL(10,2)**
* payment_date **DATETIME**
* payment_method **VARCHAR(50)**
* payment_img **VARCHAR(50)**


__alerts__
* alert_id **PK (UUID)**
* meter_id **FK (UUID)**
* alert_type **Enum (Leakage, Overconsumption, Error)**
* alert_description **VARCHAR(250)**
* alert_date **DATETIME**
* alert_Status **Enum (Pending, Resolved)**


**maintenance_logs**
* log_id **PK (UUID)**
* meter_id **FK (UUID)**
* maintenance_type **Enum (Inspection, Replacement, Repair)**
* technician_id **FK (UUID)**
* log_date **DATETIME**
* log_notes **VARCHAR(250)**