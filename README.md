# Biometric Student Attendance System

**Vendor:** Nevon Solutions
**Customer:** BioSec Educational Institution
**Document ID:** NS-AR-2026-001
**Version:** 1.0

---

## Repository Overview

This repository contains all regulated-revision requirements and requirements modelling artefacts produced during the Analysing phase. All items are prepared and ready for export into the Software Requirements Specification (SRS).

---

## Repository Structure

```
/
├── requirements/
│   ├── business-operations.md
│   └── technical.md
├── requirement-models/
│   ├── paper-napkin-model.jpg
│   ├── context-diagram.pdf
│   ├── data-dictionary.md
│   ├── ERD.pdf
│   ├── gantt-chart.png
│   └── wireframes/
│       ├── parent-mobile-app/
│       ├── teacher-mobile-app/
│       └── admin-web-portal/
└── README.md
```

---

## Requirements

All requirements are the regulated-revision output of the Analysing method, transmuted from BioSec's Project Specification through the BCIC process. Each requirement file contains the following fields per clause:

- Requirement ID 
- Requirement statement
- Rationale
- Acceptance criteria
- Dependencies
- Priority
- Status

Requirements are organised by category and ready for export into the SRS.

---

## Requirements Modelling

### 2D Paper Napkin Model
File: `requirment-models/paper-napkin-model.jpg`

A conceptual sketch produced during the BC-01 Business Clarification Session on 07/02/2026. It captures the early-stage system overview discussed with stakeholders, covering biometric verification flow, notification timing logic, leave application workflow, and compliance threshold configuration. This model informed subsequent refinements to the context diagram and data structures.

### Context Diagram (Revised)
File: `requirment-models/context-diagram.pdf`

A revised version of the Context Diagram originally provided in the BioSec Project Specification. Updated following the TC-02 Technical Clarification Session on 09/02/2026 to reflect all external system interfaces identified during analysis. The diagram shows data flows between the Biometric Student Attendance System and six external entities: Parent, Teacher, Administrator, Medical Certificate System, Firebase/APNS, Fingerprint Scanner, and School Management Database.

### Gantt Chart
File: `requirment-models/BioSec Gantt Chart.xlsx`

A project timeline chart maintained for the Project Manager, showing milestones, task durations, and delivery schedule across the full project lifecycle. 

---

### Data Dictionary Tables (Revised)
File: `requirment-models/data-dictionary.md`

A revised data dictionary updated after clarification sessions. Contains nine tables covering all core data entities. Tables C.7 (NotificationLog), C.8 (BiometricScan), and C.9 (ExternalSystemLog) are newly added to support external system integrations and clarified requirements identified during the TC-02 session.

| Table | Entity |
|---|---|
| C.1 | UserAccount |
| C.2 | Student |
| C.3 | Teacher |
| C.4 | AttendanceRecord |
| C.5 | LeaveRequest |
| C.6 | WarningLetter |
| C.7 | NotificationLog (NEW) |
| C.8 | BiometricScan (NEW) |
| C.9 | ExternalSystemLog (NEW) |

---

## ERD (Entity Relationship Diagram)
File: `requirement-models/ERD.pdf`

A full Entity Relationship Diagram for the Biometric Student Attendance Management System using crow's foot notation. Covers all nine data entities and their relationships. ExternalSystemLog is a standalone audit log with no enforced FK relationships. The diagram reflects the revised Data Dictionary (Tables C.1 to C.9).

---

## Wireframes

The wireframes folder contains UI models produced to support stakeholder demonstration during the Clarify phase, covering three platforms:

- Parent mobile application screens
- Teacher mobile application screens
- Administrator web portal screens

These wireframes will be brought into the SRS as requirements models with in-text references.

---

## Requirements Status

| Category | Status |
|---|---|
| Business Operations Requirements (BOR) | Ready for SRS |
| Technical Requirements (TR) | Ready for SRS |

Three open issues remain pending resolution before SRS finalisation. Refer to the Analysing Report (NS-AR-2026-001) for details.

---

## Team

| Name | Role |
|---|---|
| Loh Wen Xuan | Project Lead |
| Ang Ke Ying | Requirements Manager |
| Chu Wee How Brandon | Technical & Compliance Analyst |
| Haimirul Hakim Bin Hamidi | Solutions Architect |
| Lim Zong Wei Glenn | Quality Assurance Analyst |