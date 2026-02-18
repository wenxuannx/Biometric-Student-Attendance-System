# Data Dictionary (Revised)

Produced during the Analysing method. Tables C.7, C.8, and C.9 are newly added following the TC-02 Technical Clarification Session (09/02/2026) to support external system integrations and clarified requirements.

---

## Table C.1 – UserAccount

| Field Name | Data Type | Size | Allow Null | Description | Example |
|---|---|---|---|---|---|
| user_id | INT | 11 | No | PK: Unique account ID | 1001 |
| username | VARCHAR | 50 | No | Login username | admin1 |
| password_hash | VARCHAR | 256 | No | Encrypted password (SHA256 hash) | (hash) |
| role | ENUM | – | No | 'Admin', 'Parent', 'Teacher' | Parent |
| email | VARCHAR | 100 | No | Registered email for notifications | parent@school.sg |
| created_date | DATETIME | – | No | Account creation timestamp | 2026-01-01 10:00:00 |

---

## Table C.2 – Student

| Field Name | Data Type | Size | Allow Null | Description | Example |
|---|---|---|---|---|---|
| student_id | INT | 11 | No | PK: Unique student ID | 2026001 |
| first_name | VARCHAR | 50 | No | Given name | Ah |
| last_name | VARCHAR | 50 | No | Family name | Mei |
| date_of_birth | DATE | – | No | Birth date | 2010-05-15 |
| fingerprint_hash | VARCHAR | 256 | No | Biometric hash for attendance matching | (hash) |
| parent_id | INT | 11 | No | FK to UserAccount (parent account) | 2001 |
| status | VARCHAR | 20 | Yes | Active, Inactive, Suspended | Active |

---

## Table C.3 – Teacher

| Field Name | Data Type | Size | Allow Null | Description | Example |
|---|---|---|---|---|---|
| teacher_id | INT | 11 | No | PK: Unique teacher ID | T001 |
| first_name | VARCHAR | 50 | No | Given name | Mr. Tan |
| last_name | VARCHAR | 50 | No | Family name | Wei |
| user_id | INT | 11 | No | FK to UserAccount | 3001 |
| contact_phone | VARCHAR | 15 | Yes | Phone for notifications | +6581234567 |

---

## Table C.4 – AttendanceRecord

| Field Name | Data Type | Size | Allow Null | Description | Example |
|---|---|---|---|---|---|
| attendance_id | INT | 11 | No | PK: Unique record ID | 500001 |
| student_id | INT | 11 | No | FK to Student | 2026001 |
| teacher_id | INT | 11 | No | FK to Teacher | T001 |
| lecture_datetime | DATETIME | – | No | Scheduled lecture start | 2026-02-03 09:00:00 |
| entry_time | DATETIME | – | Yes | Biometric entry scan time | 2026-02-03 09:01:30 |
| exit_time | DATETIME | – | Yes | Biometric exit scan time | 2026-02-03 10:25:45 |
| status | ENUM | – | No | Present, Late, Absent, Excused | Present |
| leave_id | INT | 11 | Yes | FK to LeaveRequest (if Excused) | 7001 |

---

## Table C.5 – LeaveRequest

| Field Name | Data Type | Size | Allow Null | Description | Example |
|---|---|---|---|---|---|
| leave_id | INT | 11 | No | PK: Unique leave request ID | 7001 |
| student_id | INT | 11 | No | FK to Student | 2026001 |
| parent_id | INT | 11 | No | FK to UserAccount (requester) | 2001 |
| start_date | DATE | – | No | Leave start date | 2026-02-05 |
| end_date | DATE | – | No | Leave end date | 2026-02-07 |
| reason | TEXT | – | No | Brief reason | Sick leave |
| mc_reference | VARCHAR | 100 | Yes | MCS reference for medical cert | MCS-2026-001 |
| status | ENUM | – | No | Pending, Approved, Rejected, Cancelled | Approved |
| admin_note | TEXT | – | Yes | Admin response or comments | Approved with MC |
| request_date | DATETIME | – | No | Timestamp of request | 2026-02-04 14:30:00 |

---

## Table C.6 – WarningLetter

| Field Name | Data Type | Size | Allow Null | Description | Example |
|---|---|---|---|---|---|
| warning_id | INT | 11 | No | PK: Unique warning ID | 8001 |
| student_id | INT | 11 | No | FK to Student | 2026001 |
| parent_id | INT | 11 | No | FK to UserAccount (recipient) | 2001 |
| issue_date | DATE | – | No | Date warning issued | 2026-02-10 |
| attendance_pct | DECIMAL | 5,2 | No | Attendance percentage triggering warning | 75.50 |
| message | TEXT | – | No | Warning content | Improve attendance |
| parent_reply | TEXT | – | Yes | Parent response | Will monitor |

---

## Table C.7 – NotificationLog (NEW)

| Field Name | Data Type | Size | Allow Null | Description | Example |
|---|---|---|---|---|---|
| notification_id | INT | 11 | No | PK: Unique notification ID | 5001 |
| user_id | INT | 11 | No | FK to UserAccount (recipient) | 2001 |
| notification_type | ENUM | – | No | attendance_alert, leave_status, compliance | attendance_alert |
| delivery_channel | ENUM | – | No | firebase, apns, smtp, sms_gateway | firebase |
| sent_timestamp | DATETIME | – | No | When notification sent | 2026-02-10 09:15:00 |
| delivery_status | ENUM | – | No | sent, delivered, failed | delivered |
| delivery_timestamp | DATETIME | – | Yes | When delivery confirmed | 2026-02-10 09:15:23 |
| retry_count | INT | 2 | No | Number of retry attempts | 1 |
| fallback_triggered | BOOLEAN | – | No | SMS fallback activated after 30 min | 0 |
| message_content | TEXT | – | No | Notification message body | Your child was absent today |
| reference_id | INT | 11 | Yes | FK to related record | 3001 |

---

## Table C.8 – BiometricScan (NEW)

| Field Name | Data Type | Size | Allow Null | Description | Example |
|---|---|---|---|---|---|
| scan_id | INT | 11 | No | PK: Unique scan ID | 600001 |
| student_id | INT | 11 | No | FK to Student | 2026001 |
| device_id | VARCHAR | 50 | No | Biometric device identifier | BIO-DEVICE-01 |
| scan_timestamp | DATETIME | – | No | When scan occurred | 2026-02-10 09:01:15 |
| verification_result | ENUM | – | No | success, failed, retry | success |
| retry_count | INT | 2 | No | Number of retry attempts | 0 |
| manual_override | BOOLEAN | – | No | Manual attendance authorised | 0 |
| processing_time_ms | INT | 6 | No | Scan processing time in ms | 1850 |
| fingerprint_quality | DECIMAL | 3,2 | Yes | Quality score (0-1) | 0.92 |

---

## Table C.9 – ExternalSystemLog (NEW)

| Field Name | Data Type | Size | Allow Null | Description | Example |
|---|---|---|---|---|---|
| log_id | INT | 11 | No | PK: Unique log entry ID | 11001 |
| system_name | ENUM | – | No | mcs, firebase, apns, smtp, sms | mcs |
| request_timestamp | DATETIME | – | No | When request sent | 2026-02-10 09:20:00 |
| response_timestamp | DATETIME | – | Yes | When response received | 2026-02-10 09:20:04 |
| request_type | VARCHAR | 50 | No | API endpoint or operation | validate_mc |
| response_status | ENUM | – | No | success, timeout, error, unavailable | success |
| retry_attempt | INT | 2 | No | Retry attempt number | 1 |
| error_message | TEXT | – | Yes | Error details if failed | Connection timeout |