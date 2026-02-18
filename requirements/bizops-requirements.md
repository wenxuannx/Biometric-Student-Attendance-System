# Business Operations Requirements

---

## BOR Level 0 – System Access Platform

### BOR-0-01

| Field | Content |
|---|---|
| Requirement ID | BOR-0-01 |
| Requirement Statement | The system shall provide role-based access control for Administrators, Teachers, and Parents across all five BioSec campuses. |
| Rationale | Retained from PS. Clear access definitions with appropriate role separation and authentication requirements. |
| Acceptance Criteria | Each user role can only access functions assigned to that role. Unauthorised access attempts are rejected and logged. |
| Dependencies | TR-0-02, TR-1-CL-01, TR-1-CL-02 |
| Priority | High |
| Status | Ready for SRS |

---

### BOR-0-02

| Field | Content |
|---|---|
| Requirement ID | BOR-0-02 |
| Requirement Statement | The system shall provide Administrators with access to the following functions: user account management, attendance report generation, compliance threshold configuration, and leave request review. |
| Rationale | Revised from PS. Original stated "administration activities" without listing specific functions, making it ambiguous and untestable. |
| Acceptance Criteria | All four listed functions are accessible to Administrator role only. Each function is operable from the web portal. |
| Dependencies | BOR-1-WEB-01, BOR-1-WEB-02 |
| Priority | High |
| Status | Ready for SRS |

---

### BOR-0-03

| Field | Content |
|---|---|
| Requirement ID | BOR-0-03 |
| Requirement Statement | The system shall comply with the Personal Data Protection Act (PDPA) for all collection, storage, processing, and transmission of student biometric and attendance data. |
| Rationale | Retained from PS. Appropriate abstraction without prescribing technical implementation. PDPA compliance reference is correct. |
| Acceptance Criteria | All data handling operations are auditable. Parental consent is collected before biometric enrolment. Data subject access requests are fulfilled within 30 days. |
| Dependencies | TR-1-BE-05b, TR-1-DOC-01 |
| Priority | High |
| Status | Ready for SRS |

---

## BOR Level 1 – Attendance

### BOR-1-ATT-01 (Revised)

| Field | Content |
|---|---|
| Requirement ID | BOR-1-ATT-01 |
| Requirement Statement | The system shall verify student identity via biometric fingerprint scan within 2 seconds, supporting 50 students per device per 10 minutes. After 3 failed scan retries, the system shall authorise manual attendance entry with a separate flag recorded against that entry. |
| Rationale | Revised from PS. Original used "quickly" without quantifiable time limits, making it untestable. Performance figures confirmed in BC-01 clarification session (07/02/2026). |
| Acceptance Criteria | Biometric verification completes within 2 seconds under normal operating conditions. Devices support 50 students per 10-minute period. After exactly 3 failed retries, manual override is offered and the resulting attendance record is flagged. |
| Dependencies | TR-1-BE-01b, TR-1-BE-01c, C.8 BiometricScan |
| Priority | High |
| Status | Ready for SRS |

---

### BOR-1-ATT-02

| Field | Content |
|---|---|
| Requirement ID | BOR-1-ATT-02 |
| Requirement Statement | The system shall record the attendance result and provide immediate feedback to the student following each biometric scan attempt. |
| Rationale | Retained from PS. Clear attendance result recording requirement with immediate feedback constraint, without prescribing UI design. |
| Acceptance Criteria | Attendance result is recorded in the database immediately after each scan. Feedback is delivered to the student within the same 2-second verification window. |
| Dependencies | BOR-1-ATT-01, C.4 AttendanceRecord |
| Priority | High |
| Status | Ready for SRS |

---

## BOR Level 1 – Mobile Application

### BOR-1-MOB-01

| Field | Content |
|---|---|
| Requirement ID | BOR-1-MOB-01 |
| Requirement Statement | The system shall comply with BioSec's institutional data access policies for all mobile application data retrieval operations. |
| Rationale | Revised from PS. Original referenced "institutional policies" without citing specific policy documents. Flagged for specific policy references to be confirmed by BioSec and incorporated into SRS. |
| Acceptance Criteria | All data retrieval operations enforce role-based access. Access outside assigned role is rejected and logged. |
| Dependencies | BOR-0-01, BOR-0-03 |
| Priority | Medium |
| Status | Ready for SRS |

---

### BOR-1-MOB-02a

| Field | Content |
|---|---|
| Requirement ID | BOR-1-MOB-02a |
| Parent ID | BOR-1-MOB-02 |
| Requirement Statement | The system shall provide parents with access to attendance information for their child only. |
| Rationale | Decomposed from compound requirement BOR-1-MOB-02, which combined parent access, teacher access, sync timing, and accuracy criteria into a single untestable statement. |
| Acceptance Criteria | A parent account can view attendance records for their linked child only. Attempts to access another student's records are rejected. |
| Dependencies | BOR-0-01, C.1 UserAccount, C.4 AttendanceRecord |
| Priority | High |
| Status | Ready for SRS |

---

### BOR-1-MOB-02b

| Field | Content |
|---|---|
| Requirement ID | BOR-1-MOB-02b |
| Parent ID | BOR-1-MOB-02 |
| Requirement Statement | The system shall provide teachers with access to attendance information for their assigned classes only. |
| Rationale | Decomposed from compound requirement BOR-1-MOB-02. |
| Acceptance Criteria | A teacher account can view attendance records for their assigned classes only. Attempts to access unassigned class records are rejected. |
| Dependencies | BOR-0-01, C.3 Teacher, C.4 AttendanceRecord |
| Priority | High |
| Status | Ready for SRS |

---

### BOR-1-MOB-02c (Revised)

| Field | Content |
|---|---|
| Requirement ID | BOR-1-MOB-02c |
| Parent ID | BOR-1-MOB-02 |
| Requirement Statement | The system shall synchronise attendance data every 5 minutes, with a maximum data staleness of 30 minutes. |
| Rationale | Decomposed and revised from BOR-1-MOB-02. Original lacked acceptable latency or sync intervals. Figures confirmed in BC-01 clarification session (07/02/2026). |
| Acceptance Criteria | Attendance data displayed on mobile is no more than 30 minutes old. Sync occurs every 5 minutes when connectivity is available. |
| Dependencies | TR-1-BE-01, TR-1-CL-01c |
| Priority | High |
| Status | Ready for SRS |

---

### BOR-1-MOB-03a

| Field | Content |
|---|---|
| Requirement ID | BOR-1-MOB-03a |
| Parent ID | BOR-1-MOB-03 |
| Requirement Statement | The system shall enable parents to submit leave requests for attendance-related absences, with mandatory field validation and a save-as-draft function that preserves incomplete submissions for 7 days. |
| Rationale | Decomposed from compound requirement BOR-1-MOB-03. Draft preservation period confirmed in BC-01 clarification session (07/02/2026). |
| Acceptance Criteria | Leave request form validates all mandatory fields with field-level error messages. Incomplete drafts are saved and retrievable for 7 days. |
| Dependencies | C.5 LeaveRequest |
| Priority | High |
| Status | Ready for SRS |

---

### BOR-1-MOB-03b

| Field | Content |
|---|---|
| Requirement ID | BOR-1-MOB-03b |
| Parent ID | BOR-1-MOB-03 |
| Requirement Statement | The system shall validate leave requests with medical certificates via REST API call to the Medical Certificate System (MCS). Leave requests shall queue during MCS outage, with a manual override available. Requests pending beyond 4 hours shall be flagged for manual review. |
| Rationale | Decomposed from compound requirement BOR-1-MOB-03. MCS outage handling confirmed in BC-01 clarification session (07/02/2026). |
| Acceptance Criteria | MCS validation is called for each leave request with an attached MC. During MCS outage, requests enter a queue. Any request in queue beyond 4 hours is flagged. Manual override is available to authorised administrators. |
| Dependencies | TR-1-BE-02, C.5 LeaveRequest, C.9 ExternalSystemLog |
| Priority | High |
| Status | Ready for SRS |

---

### BOR-1-MOB-04 (Revised)

| Field | Content |
|---|---|
| Requirement ID | BOR-1-MOB-04 |
| Requirement Statement | The system shall deliver push notifications to parents and teachers for attendance events and leave status updates, achieving 98% delivery within 15 minutes. If delivery fails within 30 minutes, the system shall send an SMS fallback. |
| Rationale | Revised from PS. Original lacked delivery time SLAs, success percentage, and measurement methodology. Figures confirmed in BC-01 clarification session (07/02/2026). |
| Acceptance Criteria | 98% of notifications are delivered within 15 minutes. SMS fallback is triggered automatically after 30 minutes of failed delivery. Delivery status is logged for each notification. |
| Dependencies | TR-1-BE-01, C.7 NotificationLog |
| Priority | High |
| Status | Ready for SRS |

---

## BOR Level 1 – Web Application (Administrator Portal)

### BOR-1-WEB-01a

| Field | Content |
|---|---|
| Requirement ID | BOR-1-WEB-01a |
| Parent ID | BOR-1-WEB-01 |
| Requirement Statement | The system shall restrict attendance information access to users with authorised administrative roles only. |
| Rationale | Decomposed from compound requirement BOR-1-WEB-01, which combined data access, authorisation, and compliance threshold enforcement into one statement. |
| Acceptance Criteria | Only accounts with the Administrator role can access attendance records via the web portal. Non-administrator access attempts are rejected and logged. |
| Dependencies | BOR-0-01, C.1 UserAccount, C.4 AttendanceRecord |
| Priority | High |
| Status | Ready for SRS |

---

### BOR-1-WEB-01b

| Field | Content |
|---|---|
| Requirement ID | BOR-1-WEB-01b |
| Parent ID | BOR-1-WEB-01 |
| Requirement Statement | The system shall issue compliance warnings when a student's attendance falls below the 80% threshold per term. The threshold shall be configurable by administrators. |
| Rationale | Decomposed from BOR-1-WEB-01. Threshold default confirmed in BC-01 clarification session (07/02/2026). |
| Acceptance Criteria | Compliance warnings are generated automatically when attendance drops below the configured threshold. Default threshold is 80%. Administrators can adjust the threshold from the web portal. |
| Dependencies | BOR-1-WEB-01a, C.6 WarningLetter |
| Priority | High |
| Status | Ready for SRS |

---

### BOR-1-WEB-02a

| Field | Content |
|---|---|
| Requirement ID | BOR-1-WEB-02a |
| Parent ID | BOR-1-WEB-02 |
| Requirement Statement | The system shall restrict leave approval actions to users with authorised administrative roles only. |
| Rationale | Decomposed from compound requirement BOR-1-WEB-02, which combined review capability, authorisation, and validation enforcement. |
| Acceptance Criteria | Only Administrator accounts can approve or reject leave requests. Approval actions by non-administrators are rejected and logged. |
| Dependencies | BOR-0-01, C.1 UserAccount, C.5 LeaveRequest |
| Priority | High |
| Status | Ready for SRS |

---

### BOR-1-WEB-02b

| Field | Content |
|---|---|
| Requirement ID | BOR-1-WEB-02b |
| Parent ID | BOR-1-WEB-02 |
| Requirement Statement | The system shall prevent approval of leave applications with medical certificates that failed MCS validation. |
| Rationale | Decomposed from BOR-1-WEB-02. Ensures MCS validation outcome is enforced at the point of administrator approval. |
| Acceptance Criteria | Leave requests with failed MCS validation are locked from approval. Administrator receives a clear validation failure reason. Manual override by a senior administrator is logged with justification. |
| Dependencies | BOR-1-MOB-03b, TR-1-BE-02, C.5 LeaveRequest |
| Priority | High |
| Status | Ready for SRS |