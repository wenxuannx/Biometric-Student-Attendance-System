# Technical Requirements

---

## TR Level 0 – Technical Execution Platforms

### TR-0-01 (Revised)

| Field | Content |
|---|---|
| Requirement ID | TR-0-01 |
| Requirement Statement | The system shall support native mobile applications on Android (minimum Android 10) and iOS (minimum iOS 14), and a web portal accessible on current versions of Chrome, Safari, Firefox, and Edge. |
| Rationale | Revised from PS. Original specified native mobile apps without minimum OS versions or device specs, making it incomplete and untestable. Minimum versions confirmed in TC-02 clarification session (09/02/2026). |
| Acceptance Criteria | Mobile applications install and operate correctly on Android 10 and above, and iOS 14 and above. Web portal functions correctly on current versions of all four listed browsers. |
| Dependencies | TR-1-CL-01, TR-1-CL-02 |
| Priority | High |
| Status | Ready for SRS |

---

### TR-0-02 (Revised)

| Field | Content |
|---|---|
| Requirement ID | TR-0-02 |
| Requirement Statement | The system shall be hosted on Microsoft Azure cloud infrastructure in the Singapore region, accessible via HTTPS with TLS 1.2 or higher. |
| Rationale | Revised from PS. Original lacked URL format, HTTPS specification, and access scope. Azure Singapore region specification confirmed in TC-02 clarification session (09/02/2026). |
| Acceptance Criteria | System is deployed on Azure Singapore region. All endpoints are accessible via HTTPS only. TLS version is 1.2 or higher. HTTP requests are redirected to HTTPS. |
| Dependencies | TR-1-BE-01a |
| Priority | High |
| Status | Ready for SRS |

---

## TR Level 1 – Backend Infrastructure

### TR-1-BE-01a

| Field | Content |
|---|---|
| Requirement ID | TR-1-BE-01a |
| Parent ID | TR-1-BE-01 |
| Requirement Statement | The system shall be hosted on Microsoft Azure cloud infrastructure. |
| Rationale | Decomposed from compound requirement TR-1-BE-01, which combined hosting platform, user concurrency, and scan concurrency. |
| Acceptance Criteria | All system components are deployed on Microsoft Azure. No components are hosted on non-Azure infrastructure without documented justification. |
| Dependencies | TR-0-02 |
| Priority | High |
| Status | Ready for SRS |

---

### TR-1-BE-01b

| Field | Content |
|---|---|
| Requirement ID | TR-1-BE-01b |
| Parent ID | TR-1-BE-01 |
| Requirement Statement | The system shall support a minimum of 1,500 concurrent authenticated users with graceful degradation up to 2,000 users at a maximum 4-second response time. Auto-scaling shall trigger at 70% CPU utilisation. |
| Rationale | Decomposed and revised from TR-1-BE-01. Original used a vague 1000+ threshold. Figures confirmed in TC-02 (09/02/2026). |
| Acceptance Criteria | System maintains normal response times up to 1,500 concurrent users. Response time does not exceed 4 seconds at 2,000 users. Auto-scaling activates at 70% CPU. |
| Dependencies | TR-0-02, TR-1-BE-01a |
| Priority | High |
| Status | Ready for SRS |

---

### TR-1-BE-01c

| Field | Content |
|---|---|
| Requirement ID | TR-1-BE-01c |
| Parent ID | TR-1-BE-01 |
| Requirement Statement | The system shall process 200 concurrent biometric scans with a response time under 2 seconds per scan. |
| Rationale | Decomposed from TR-1-BE-01. Separated from user concurrency for independent testability. |
| Acceptance Criteria | 200 simultaneous biometric scan requests are processed without queuing. Each scan completes within 2 seconds. |
| Dependencies | BOR-1-ATT-01, C.8 BiometricScan |
| Priority | High |
| Status | Ready for SRS |

---

### TR-1-BE-02 (Revised)

| Field | Content |
|---|---|
| Requirement ID | TR-1-BE-02 |
| Requirement Statement | The system shall integrate with BioSec's Medical Certificate System via HTTPS REST API with OAuth 2.0 authentication, a 5-second timeout, 3 retry attempts with exponential backoff, and a 99.5% SLA. |
| Rationale | Revised from PS. Original stated 99.999% uptime which is technically infeasible, and lacked API authentication, timeout, and retry specifications. Confirmed in TC-02 (09/02/2026). |
| Acceptance Criteria | Integration uses HTTPS REST with OAuth 2.0. Timeout is 5 seconds. System retries up to 3 times with exponential backoff before logging failure. MCS achieves 99.5% uptime over any rolling 30-day period. |
| Dependencies | BOR-1-MOB-03b, C.9 ExternalSystemLog |
| Priority | High |
| Status | Ready for SRS |

---

### TR-1-BE-03 (Revised)

| Field | Content |
|---|---|
| Requirement ID | TR-1-BE-03 |
| Requirement Statement | The system shall encrypt all biometric data at rest using AES-256 and all data in transit using TLS 1.2 or higher. |
| Rationale | Revised from PS. Original referenced "security controls" without specifying algorithms. Confirmed in TC-02 (09/02/2026). |
| Acceptance Criteria | All biometric data in the database is AES-256 encrypted. All transmitted data uses TLS 1.2 or higher. Encryption keys are managed separately from encrypted data. |
| Dependencies | TR-0-02, TR-1-BE-05b |
| Priority | High |
| Status | Ready for SRS |

---

### TR-1-BE-04 (Revised)

| Field | Content |
|---|---|
| Requirement ID | TR-1-BE-04 |
| Requirement Statement | The system shall achieve a False Acceptance Rate (FAR) of no more than 0.01% based on commercial fingerprint sensor capabilities in high-traffic educational environments. |
| Rationale | Revised from PS. Original specified 0.001% FAR which is technically infeasible for commercial sensors. Confirmed in TC-02 (09/02/2026). |
| Acceptance Criteria | FAR does not exceed 0.01% under testing conditions replicating high-traffic educational use, measured over a minimum of 10,000 scan attempts. |
| Dependencies | BOR-1-ATT-01, C.8 BiometricScan |
| Priority | High |
| Status | Ready for SRS |

---

### TR-1-BE-05a

| Field | Content |
|---|---|
| Requirement ID | TR-1-BE-05a |
| Parent ID | TR-1-BE-05 |
| Requirement Statement | The system shall use a SQL Server database with a complete schema and stored procedures for all data operations. |
| Rationale | Decomposed from compound TR-1-BE-05, which combined database, encryption, and backup specifications. |
| Acceptance Criteria | All data operations use SQL Server. Schema covers all entities in Tables C.1 to C.9. Stored procedures are used for all core operations. |
| Dependencies | C.1–C.9 Data Dictionary |
| Priority | High |
| Status | Ready for SRS |

---

### TR-1-BE-05b

| Field | Content |
|---|---|
| Requirement ID | TR-1-BE-05b |
| Parent ID | TR-1-BE-05 |
| Requirement Statement | The system shall encrypt all biometric data stored in the database using AES-256 encryption. |
| Rationale | Decomposed from TR-1-BE-05. |
| Acceptance Criteria | All biometric fields are stored in AES-256 encrypted form. Decryption is only possible by authorised system components using managed keys. |
| Dependencies | TR-1-BE-03, C.2 Student |
| Priority | High |
| Status | Ready for SRS |

---

### TR-1-BE-05c

| Field | Content |
|---|---|
| Requirement ID | TR-1-BE-05c |
| Parent ID | TR-1-BE-05 |
| Requirement Statement | The system shall perform daily automated backups of the database. |
| Rationale | Decomposed from TR-1-BE-05. |
| Acceptance Criteria | Automated backup runs daily. Backup completion is logged. Restore from backup is tested at least quarterly. |
| Dependencies | TR-1-BE-05a |
| Priority | High |
| Status | Ready for SRS |

---

### TR-1-CPR-01 (Revised)

| Field | Content |
|---|---|
| Requirement ID | TR-1-CPR-01 |
| Requirement Statement | The system shall implement account lockout after a configurable number of failed login attempts, with a defined lockout duration, account unlock process, administrator alerts, and audit logging of all lockout events. |
| Rationale | Revised from PS. Original specified lockout without resolution procedures, duration, or audit logging. |
| Acceptance Criteria | Account locks after configured failed attempts. Lockout duration is configurable. Administrators can unlock accounts. All lockout events are logged with timestamp and account identifier. |
| Dependencies | BOR-0-01, C.1 UserAccount |
| Priority | Medium |
| Status | Ready for SRS |

---

### TR-1-CPR-04 (Revised)

| Field | Content |
|---|---|
| Requirement ID | TR-1-CPR-04 |
| Requirement Statement | The system shall classify operational issues using a three-tier severity model: Critical (4-hour response, 24-hour resolution), High (8-hour response, 48-hour resolution), and Medium (24-hour response, 5-day resolution). |
| Rationale | Revised from PS. Original lacked criticality levels, making SLA enforcement untestable. Tiers confirmed in TC-02 (09/02/2026). |
| Acceptance Criteria | All reported issues are classified at time of logging. Response and resolution SLAs are tracked per tier. SLA breaches generate escalation alerts. |
| Dependencies | None |
| Priority | Medium |
| Status | Ready for SRS |

---

## TR Level 1 – Client Applications

### TR-1-CL-01a

| Field | Content |
|---|---|
| Requirement ID | TR-1-CL-01a |
| Parent ID | TR-1-CL-01 |
| Requirement Statement | The system shall include an Android application developed with Kotlin and distributed via the Google Play Store. |
| Rationale | Decomposed from compound TR-1-CL-01 for independent testability per platform. |
| Acceptance Criteria | Android application is built using Kotlin. Application is available on the Google Play Store under BioSec's developer account. |
| Dependencies | TR-0-01 |
| Priority | High |
| Status | Ready for SRS |

---

### TR-1-CL-01b

| Field | Content |
|---|---|
| Requirement ID | TR-1-CL-01b |
| Parent ID | TR-1-CL-01 |
| Requirement Statement | The system shall include an iOS application developed with Swift and distributed via the Apple App Store. |
| Rationale | Decomposed from compound TR-1-CL-01. |
| Acceptance Criteria | iOS application is built using Swift. Application is available on the Apple App Store under BioSec's developer account. |
| Dependencies | TR-0-01 |
| Priority | High |
| Status | Ready for SRS |

---

### TR-1-CL-01c

| Field | Content |
|---|---|
| Requirement ID | TR-1-CL-01c |
| Parent ID | TR-1-CL-01 |
| Requirement Statement | The mobile applications shall support offline data access with automatic synchronisation when connectivity restores, with a maximum offline duration of 48 hours and a local storage limit of 50MB. |
| Rationale | Decomposed from TR-1-CL-01. Offline duration and storage limit confirmed in TC-02 (09/02/2026). |
| Acceptance Criteria | Attendance viewing and leave request drafting are available offline. Data synchronises automatically when connectivity is restored. Offline mode does not exceed 48 hours. Local cache does not exceed 50MB. |
| Dependencies | BOR-1-MOB-02c |
| Priority | High |
| Status | Ready for SRS |

---

### TR-1-CL-01d

| Field | Content |
|---|---|
| Requirement ID | TR-1-CL-01d |
| Parent ID | TR-1-CL-01 |
| Requirement Statement | The mobile applications shall be code-signed with BioSec institutional certificates. |
| Rationale | Decomposed from TR-1-CL-01. |
| Acceptance Criteria | Both Android and iOS applications are signed with BioSec-issued certificates prior to distribution. |
| Dependencies | TR-1-CL-01a, TR-1-CL-01b |
| Priority | Medium |
| Status | Ready for SRS |

---

### TR-1-CL-01e

| Field | Content |
|---|---|
| Requirement ID | TR-1-CL-01e |
| Parent ID | TR-1-CL-01 |
| Requirement Statement | Mobile application updates shall maintain backward compatibility during the 12-month warranty period. |
| Rationale | Decomposed from TR-1-CL-01. |
| Acceptance Criteria | No update during the warranty period breaks functionality for users on the minimum supported OS versions. |
| Dependencies | TR-0-01 |
| Priority | Medium |
| Status | Ready for SRS |

---

### TR-1-CL-01f

| Field | Content |
|---|---|
| Requirement ID | TR-1-CL-01f |
| Parent ID | TR-1-CL-01 |
| Requirement Statement | The mobile applications shall encrypt all locally stored data using AES-256 encryption. |
| Rationale | Decomposed from TR-1-CL-01. |
| Acceptance Criteria | All data written to local storage on device is AES-256 encrypted. Unencrypted data is not written to device storage at any point. |
| Dependencies | TR-1-BE-03 |
| Priority | High |
| Status | Ready for SRS |

---

### TR-1-CL-02

| Field | Content |
|---|---|
| Requirement ID | TR-1-CL-02 |
| Requirement Statement | The system shall include a web portal for administrators, accessible via modern browsers as defined in TR-0-01, with role-based access control enforced at the application layer. |
| Rationale | Retained from PS. Defines web portal boundaries with complete security and distribution specifications. |
| Acceptance Criteria | Web portal is accessible on all browsers listed in TR-0-01. Role-based access is enforced. Administrators cannot access functions outside their role. |
| Dependencies | TR-0-01, BOR-0-01 |
| Priority | High |
| Status | Ready for SRS |

---

## TR Level 1 – Documentation

### TR-1-DOC-01

| Field | Content |
|---|---|
| Requirement ID | TR-1-DOC-01 |
| Requirement Statement | The vendor shall deliver documented source code with inline comments, a README, and a build guide, with institutional ownership transferred to BioSec upon project completion. |
| Rationale | Retained from PS. Comprehensively defines source code documentation deliverable with institutional ownership. |
| Acceptance Criteria | Source code includes inline comments for all non-trivial logic. README and build guide are present in the repository. Ownership transfer is confirmed in the handover sign-off. |
| Dependencies | None |
| Priority | High |
| Status | Ready for SRS |

---

### TR-1-DOC-02

| Field | Content |
|---|---|
| Requirement ID | TR-1-DOC-02 |
| Requirement Statement | The vendor shall deliver a database documentation package including the entity-relationship diagram, schema definitions, and stored procedure documentation, with institutional ownership transferred to BioSec upon project completion. |
| Rationale | Retained from PS. Defines database documentation deliverable with institutional ownership. |
| Acceptance Criteria | ERD, schema definitions, and stored procedure documentation are delivered. All tables and relationships in Tables C.1 to C.9 of the Data Dictionary are represented. Ownership transfer confirmed at handover. |
| Dependencies | TR-1-BE-05a, C.1–C.9 Data Dictionary |
| Priority | High |
| Status | Ready for SRS |

---

### TR-1-DOC-03

| Field | Content |
|---|---|
| Requirement ID | TR-1-DOC-03 |
| Requirement Statement | The vendor shall deliver API documentation covering all endpoints, request and response formats, authentication requirements, and error codes, with institutional ownership transferred to BioSec upon project completion. |
| Rationale | Retained from PS. Defines API documentation deliverable with institutional ownership. |
| Acceptance Criteria | All API endpoints are documented. Request and response formats, authentication, and error codes are included. Documentation is delivered in a format accessible to BioSec's IT team. Ownership transfer confirmed at handover. |
| Dependencies | TR-1-BE-02 |
| Priority | High |
| Status | Ready for SRS |

---

### TR-1-DOC-04

| Field | Content |
|---|---|
| Requirement ID | TR-1-DOC-04 |
| Requirement Statement | The vendor shall deliver a user manual suite covering Administrator, Teacher, and Parent roles, with institutional ownership transferred to BioSec upon project completion. |
| Rationale | Retained from PS. Defines user manual deliverable with role coverage and institutional ownership. |
| Acceptance Criteria | Separate user manuals are provided for Administrator, Teacher, and Parent roles. Each manual covers all functions available to that role. Ownership transfer confirmed at handover. |
| Dependencies | BOR-0-01 |
| Priority | High |
| Status | Ready for SRS |