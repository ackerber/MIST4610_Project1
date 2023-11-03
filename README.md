# MIST4610_Project1

## Team Name
Group 4

## Team Members
Ethan Berry  
Esha Bhat  
Anna Kerber  
Pranay Patel  
Rafe Rynne  
Jameson Shi

## Problem Description

Georgia Emergency Medical Center needed a database portraying the relationships between many different entities, involving attributes and identifiers. It is extremely important for this database to exist so that proper prescriptions are in place, proper treatment is given, and diagnoses are recorded correctly. The central entity of the database is the Patients entity - this is because patients are the heart of every hospital and are the reason it exists, and conjoins to nearly half of the entities in the diagram. We are interested in accurately portraying this relationship and producing queries that solve important questions that the hospital may have to answer in the future. 

## Data Model

The "Patients" entity serves as a central component of the database. It has a one-to-many relationship with "Medical Records," meaning that each patient can have multiple medical records associated with different visits. Additionally, there's a one-to-one relationship with "Emergency Contacts" to store essential contact information for each patient.

The "Medical Staff" entity represents healthcare professionals working at the clinic. It has a one-to-many relationship with "Appointments," as each staff member can have multiple appointments. Similarly, it has a one-to-many relationship with "Medical Records" since they are responsible for documenting patient interactions and treatments.

"Medical Records" are associated with both patients and medical staff. This many-to-one relationship links each medical record to a specific patient and the attending medical staff member who created it. This relationship ensures that each medical record is attributed to the correct patient and responsible medical professional.

The "Appointments" entity relates to both patients and medical staff, with many-to-one relationships. It ties specific appointments to individual patients and medical staff members, allowing for effective scheduling and tracking of patient visits.

“Emergency Contacts”: Each patient has a one-to-one relationship with their emergency contacts, storing important contact information for emergencies. This relationship ensures that each patient's vital contact information is readily available when needed.

"Suppliers" have a one-to-many relationship with "Inventory" to manage the supply chain. Each supplier can provide multiple items in the inventory, simplifying procurement and tracking.

The "Inventory" entity is connected to suppliers through a many-to-one relationship. It helps in keeping track of available medical supplies and equipment, allowing efficient inventory management.

“Billing records” have a many-to-one relationship with patients, associating each billing record with a specific patient. This relationship helps in tracking the financial aspects of patient care and payments.

“Facilities” have a one-to-many relationship with "Medical Equipment" to keep track of the equipment available in each facility. This relationship assists in organizing and maintaining the clinic's equipment.

“Medical equipment” is associated with facilities through a many-to-one relationship. It ensures that the equipment in each facility is appropriately documented and maintained.

"Prescriptions" have many-to-one relationships with both patients and medical staff. This relationship links each prescription to a specific patient and the prescribing medical professional.

“Emergency transport” records are associated with medical staff in a one-to-many relationship, indicating which medical staff members were involved in specific emergency transport incidents.

![model](https://github.com/ackerber/MIST4610_Project1/assets/95188765/40606d4d-ad9a-4067-b201-4f7ffc0583af)


## Data Dictionary

Table: APPOINTMENTS
| Column Name | Description | Data Type | Size | Format | Key? |
| :-----: | :---: | :---: | :---: | :---: | :---: |
| appointmentID |  Unique sequential number identifying the appointment |   CHAR | 9| 99AA99999| PK | 
| date |   Date of the appointment |  DATETIME  | | YYYY-MM-DD HH:MI:SS| |
| time |  Time of the appointment  |   VARCHAR | 45| | |
| reasonForVisit|   Reason for visiting | VARCHAR   | 300| | |
| status |  Appointment status  |  VARCHAR  | 200| | |
| staffID |  Indicates the staff member overseeing the appointment |   CHAR | 9| 99999AAAA| FK (ref. MEDICALSTAFF)|
|  patientID|  Indicates the patient in the appointment  |  CHAR  | 9| AAA999999| FK (ref. PATIENTS)|

Table: BILLINGRECORDS
| Column Name | Description | Data Type | Size | Format | Key? |
| :-----: | :---: | :---: | :---: | :---: | :---: |
| billingID |  Unique sequential number identifying the billing record  |   CHAR | 9| AA9999999| PK |
| date |  The date the bill is charged  |  DATETIME  | | YYYY-MM-DD HH:MI:SS| |
| paymentStatus|  The payment status of the bill  | VARCHAR   | 45| | |
| insuranceClaims |  Claims from insurance companies  |  VARCHAR  | 45| | |
| totalAmount |  The total amount of the bill  |   INT | | | |
|  patientID| Indicates the patient the bill is for   |  CHAR  | 9| AAA999999| FK (ref. PATIENTS)|
|  supplierID|  Indicates the supplier for the bill  |  CHAR  | 9| 999AAAAAA| FK (ref. SUPPLIERS)|

Table: EMERGENCYCONTACTS
| Column Name | Description | Data Type | Size | Format | Key? |
| :-----: | :---: | :---: | :---: | :---: | :---: |
| contactID |  Unique sequential number identifying the emergency contact |   CHAR | 9| 999999999| PK |
| fName |  The first name of the emergency contact  |  VARCHAR  | 45| | |
| lName |  The last name of the emergency contact  |   VARCHAR | 45| | |
| phone|  Phone number of the emergency contact | VARCHAR   | 45| (999) 999999| |
| address |   Address of the emergency contact |  VARCHAR  | 45| | |
|  patientID|  Indicates the patient associated with the emergency contact  |  CHAR  | 9| AAA9999999| FK (ref. PATIENTS)|

Table: EMERGENCYTRANSPORT
| Column Name | Description | Data Type | Size | Format | Key? |
| :-----: | :---: | :---: | :---: | :---: | :---: |
| transportID |  Unique sequential number identifying the emergency transport  |   CHAR | 9| 9999999AA| PK |
| transportDate |  The date the transport was used  |  DATETIME  | | YYYY-MM-DD HH:MI:SS| |
| modeOfTransport |  The mode of transport  |   VARCHAR | 45| | |
| destination|  The destination of the transport  | VARCHAR   | 45| | |
| attendingMedicalStaff |  The staff attenting the transport  |  VARCHAR  | 45| | |

Table: EQUIPMENTUSED
| Column Name | Description | Data Type | Size | Format | Key? |
| :-----: | :---: | :---: | :---: | :---: | :---: |
|  appointmentID|  Unique sequential number identifying the appointment |  CHAR  | 9| 99AA99999| FK (ref. APPOINTMENTS)|
|  equipmentID|  Unique sequential number identifying the equipment  |  CHAR  | 9|9999AAAAA | FK (ref. MEDICALEQUIPMENT)|

Table: FACILITIES
| Column Name | Description | Data Type | Size | Format | Key? |
| :-----: | :---: | :---: | :---: | :---: | :---: |
| facilityID |  Unique sequential number identifying the facility  |   CHAR | 9| 999AAA999| PK |
| facilityName |  The name of the facility  |  VARCHAR  | 45| | |
| location |  Location of the facility  |   VARCHAR | 45| | |
| roomAssignments|   Room number | VARCHAR   | 45| Room 999| |
| maintenanceSchedule |  How often maintenance is scheduled  |  VARCHAR  | 45| | |

Table: INVENTORY
| Column Name | Description | Data Type | Size | Format | Key? |
| :-----: | :---: | :---: | :---: | :---: | :---: |
| itemID |  Unique sequential number identifying the inventory item  |   CHAR | 9| AA9999999| PK |
| itemName |  The name of the item  |  VARCHAR  | 45| | |
| quantity |  The quantity of the item available  |   INT | | | |
| expiryDate|   The date the item expires | DATETIME   | | YYYY-MM-DD HH:MI:SS| |
| purchaseDate|   The date the item was purchased | DATETIME   | | YYYY-MM-DD HH:MI:SS| |
| unitPrice|  Unit price of the item  | INT   | | | |
|  supplierID|  Indicates the supplier associated with the item  |  CHAR  |9 | 999999AAA| FK (ref. SUPPLIERS)|

Table: MEDICALEQUIPMENT
| Column Name | Description | Data Type | Size | Format | Key? |
| :-----: | :---: | :---: | :---: | :---: | :---: |
| equipmentID |  Unique sequential number identifying the equipment |   CHAR | 9| 9999AAAAA| PK |
| equipmentName |  Name of the equipment  |  VARCHAR  | 45| | |
| maintenanceSchedule |  When maintenance is scheduled for  |   DATETIME | | YYYY-MM-DD HH:MI:SS| |
| lastCalibrationDate| Date the equipment was last calibrated   | DATETIME   | | YYYY-MM-DD HH:MI:SS| |
|  facilityID|  Indicates the facility associated with the equipment item  |  CHAR  | 9| 999AAA999| FK (ref. FACILITIES)|

Table: MEDICALRECORDS
| Column Name | Description | Data Type | Size | Format | Key? |
| :-----: | :---: | :---: | :---: | :---: | :---: |
| recordID |  Unique sequential number identifying the medical record  |   CHAR |9 | AAA999999| PK |
| date |  The date the medical record was created  |  DATETIME  | |YYYY-MM-DD HH:MI:SS | |
| diagnosis |  The patient's diagnosis  |   VARCHAR | 45| | |
| treatment|  The recommended treatment  | VARCHAR   | 45| | |
| medications |  The patient's medications  |  VARCHAR  | 45| | |
| testResults |  The results of medical tests  |  VARCHAR  | 45| | |
|  patientID|  Indicates the patient associated with the medical record  |  CHAR  | 9| AAA999999| FK (ref. PATIENTS)|
|  staffID|  Indicates the staff member who oversaw the medical record  |  CHAR  | 9| 99999AAAA| FK (ref. MEDICALSTAFF)|

Table: MEDICALSTAFF
| Column Name | Description | Data Type | Size | Format | Key? |
| :-----: | :---: | :---: | :---: | :---: | :---: |
| staffID |  Unique sequential number identifying the staff member  |   CHAR | 9| 99999AAAA| PK |
| fName |  The first name of the staff member  |  VARCHAR  | 45| | |
| lName |  The last name of the staff member  |   VARCHAR | 45| | |
| phone|  Phone number of the staff member  | VARCHAR   | 45| (999) 999999| |
| address |   Address of the staff member |  VARCHAR  | 45| | |
| email |  Email address of the staff member  |  VARCHAR  | 45| | |
| qualifications |  The staff member's qualifications  |  VARCHAR  | 200| | |
| shift schedule |  The shift schedule of the staff member  |  DATETIME  | | YYYY-MM-DD HH:MI:SS| |
|  transportID|  Indicates the transport the staff member is associated with  |  CHAR  | 9| 9999999AA| FK (ref. EMERGENCYTRANSPORT)|

TABLE: PATIENTS
| Column Name | Description | Data Type | Size | Format | Key? |
| :-----: | :---: | :---: | :---: | :---: | :---: |
| patientID |   Unique sequential number identifying the patient |  CHAR  | 9| AAA999999| PK|
| fName |  The first name of the patient  |  VAQRCHAR  | 45 | | |
| lName |  The last name of the patient  |  VARCHAR  | 45 | | |
| dateOfBirth |  Date the patient was born  | DATETIME | | YYYY-MM-DD HH:MI:SS| |
| phone |  Phone number of the patient  |  VARCHAR  | 45 | (999) 999999| |
| address |  Address of the patinet  |   VARCHAR | 45| | |
| email |  Email address of the patient  |  VARCHAR  | 45| | |
| medicalHistory |  The patient's previous medical history  | VARCHAR   | 45| | |
| insuranceInfo |  The patient's insurance plan  |  VARCHAR  | 45| | |

Table: PRESCRIPTIONS
| Column Name | Description | Data Type | Size | Format | Key? |
| :-----: | :---: | :---: | :---: | :---: | :---: |
| prescriptionID |  Unique sequential number identifying the prescription  |   CHAR | 9| 99| PK |
| medicationName |  Name of the medication  |  VARCHAR  | 45| | |
| dosage | Dosage of the medication   |   VARCHAR | 45| | |
| prescDate|  Date prescribed  | DATETIME   | |YYYY-MM-DD HH:MI:SS | |
|  patientID|  Indicates the patient the prescription is for  |  CHAR  |9 | AAA999999| FK (ref. PATIENTS)|
|  staffID|  Indicates the staff member that ordered the prescription  |  CHAR  | 9| 99999AAAA| FK (ref. MEDICALSTAFF)|

Table: SUPPLIERS
| Column Name | Description | Data Type | Size | Format | Key? |
| :-----: | :---: | :---: | :---: | :---: | :---: |
| supplierID |   Unique sequential number identifying the supplier |   CHAR | 9| 999999AAA| PK |
| companyName | Name of the company  |  VARCHAR  | 45| | |
| phone |   Phone number of the company |   VARCHAR | 45| (999) 999999| |
| address| Address of the company   | VARCHAR   |45 | | |
|  email|  Email address of the company  |  VARCHAR  | 45| | |

## Ten Queries


## Database Information



