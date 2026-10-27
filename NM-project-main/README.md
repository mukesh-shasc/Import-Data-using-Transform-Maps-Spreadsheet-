# ServiceNow Micro Project: Import Data using Transform Maps (Spreadsheet)

**Project Title:** Import Data using Transform Maps (Spreadsheet)  
**Platform:** ServiceNow (Global Scope)  
**Team Members:**  
- **Moorthy R** (Team Lead)  
- **Priyan N** (Member)  
- **KATHIRAVAN M** (Member)  
**Date:** October 2026  
**Project Location:** `C:\Users\priya\.gemini\antigravity\scratch\ServiceNow_Import_Data_using_Transform_Maps`

---

## 📌 Project Overview & Purpose
This micro project focuses on implementing an automated, error-free employee data migration and deduplication pipeline into the **ServiceNow** platform using **Import Sets** and **Transform Maps**.

The project simulates an enterprise real-world scenario where bulk employee records are received in Excel format (.xlsx) and must be migrated into a custom ServiceNow target table (`Employee Test` / `u_employee_test`). Using **Coalesce** deduplication on the unique key (`Employee ID`), repeated data loads intelligently update existing records instead of generating redundant entries. Furthermore, custom **Reports** (Pie, Bar, List) and an executive **Dashboard** (`Employee Analytics Dashboard`) were configured to provide real-time operational metrics.

---

## 👥 Team Roster
| Name | Role | Responsibilities |
| :--- | :--- | :--- |
| **Moorthy R** | Team Lead | Architecture Design, Transform Map Configuration & Governance |
| **Priyan N** | Team Member | ServiceNow Table Definition, Data Import Staging & Testing |
| **KATHIRAVAN M** | Team Member | Reports Generation, Dashboard Integration & Documentation |

---

## 📁 Complete Phasewise Directory Structure

```
ServiceNow_Import_Data_using_Transform_Maps/
├── README.md                                               (Master Project Guide & Navigation Steps)
├── Data Sheets/
│   ├── Sample Spreadsheet.xlsx                             (Initial load file - 15 employee records)
│   └── Sample Spreadsheet_Updated.xlsx                     (Delta test file - 4 records: 2 updates, 2 inserts)
├── Screenshots/                                            (All implementation screenshots)
│   ├── 1-2.png, 2-1.png, 2-2.png, 3-1.png, 3-2.png, 3-3.png, 4-1.png, 4-2.png, ...
├── 1. Ideation Phase/
│   ├── Brainstorming- Idea Generation- Prioritizaation Template.docx
│   ├── BrainstormingTemplate.pdf
│   ├── Define Problem Statements Template.docx
│   ├── Define Problem Statements Template.docx.pdf
│   ├── Empathy Map Canvas.docx
│   └── Empathy Map Canvas.docx.pdf
├── 2. Requirement Analysis/
│   ├── Customer Journey Map - Example.pdf
│   ├── Data Flow Diagrams and User Stories.docx
│   ├── Data Flow Diagrams and User Stories.docx.pdf
│   ├── Solution Requirements.docx
│   ├── Solution Requirements.docx.pdf
│   ├── Technology Stack - Template.docx
│   └── Technology Stack - Template.docx.pdf
├── 3. Project Design Phase/
│   ├── Problem - Solution Fit Template/
│   │   ├── Problem - Solution Fit Template - Sample.pdf
│   │   ├── Problem - Solution Fit Template v1.docx
│   │   └── Problem - Solution Fit Template v1.pdf
│   ├── Proposed Solution/
│   │   ├── Proposed Solution Template.docx
│   │   └── Proposed Solution Template.pdf
│   └── Solution Architecture/
│       ├── Solution Architecture.docx
│       └── Solution Architecture.pdf
├── 4. Project Planning Phase/
│   ├── Planning logic.docx
│   ├── Project Planning Template.docx
│   └── Project Planning Template.pdf
├── 5. Project Development Phase/
│   ├── Performance Testing/
│   │   ├── ServiceNow_Transform_Performance_Testing.docx
│   │   └── ServiceNow_Transform_Performance_Testing.pdf
│   └── User Acceptance Testing/
│       ├── UAT Report Template.pdf
│       └── User Acceptance Testing FSD.docx
└── 6. Project Documentation/
    ├── Final Report Template.pdf
    ├── FSD Documentation Format.docx
    └── FSD Documentation Format.pdf
```

---

## 🛠️ Step-by-Step Implementation Workflow

### **Phase 1: Prepare Excel Sheets**
- Created `Sample Spreadsheet.xlsx` with initial 15 employee records (SB-0001 to SB-0015).
- Created `Sample Spreadsheet_Updated.xlsx` with 4 rows to test updates (`SB-0004` name update, `SB-0010` email update) and new inserts (`SB-0016`, `SB-0017`).

### **Phase 2: Create Custom Target Table**
- **Navigation:** `Tables` > `Create New`
- **Label:** `Employee Test` | **Name:** `u_employee_test`
- **Fields Added:**
  - `Employee ID` (`u_employee_id`, String)
  - `Employee Name` (`u_employee_name`, String)
  - `Email` (`u_email`, String)
  - `Department` (`u_department`, String)
  - `Location` (`u_location`, String)

### **Phase 3: Create Import Set Staging Table**
- **Navigation:** `System Import Sets` > `Load Data`
- **Import Set Table:** `Create Table` -> Label: `Employee Import` (`u_employee_import`)
- **Source of Import:** File (`Sample Spreadsheet.xlsx`) -> Submit.

### **Phase 4: Create & Map Transform Map**
- **Transform Map Name:** `Sample Spreadsheet Import`
- **Source Table:** `Employee Import` (`u_employee_import`)
- **Target Table:** `Employee Test` (`u_employee_test`)
- **Action:** Clicked `Auto Map Matching Fields` and verified field pairs via `Mapping Assist`.

### **Phase 5: Execute Initial Transformation**
- Clicked `Transform`.
- **Result:** State: `Complete`, Completion Code: `Success`, Processed: 15, Inserts: 15, Updates: 0, Errors: 0.

### **Phase 6: Enable Coalesce Deduplication**
- **Navigation:** `System LDAP` > `Transform Maps` > `Sample Spreadsheet Import`
- Under `Field Maps`, set **Coalesce = True** on `u_employee_id` field.

### **Phase 7: Test Delta Insert & Update Execution**
- Loaded `Sample Spreadsheet_Updated.xlsx` into existing table `Employee Import`.
- Executed Transformation `Sample Spreadsheet Import`.
- **Result:** Processed: 4, Inserts: 2 (SB-0016, SB-0017), Updates: 2 (SB-0004, SB-0010), Errors: 0.
- Re-submitted same file: Processed: 4, Inserts: 0, Updates: 0, Ignored: 4 (Zero duplication verified!).

### **Phase 8: Create Reports**
- **Report 1 (Pie Chart):** `Employees by Department` | Group By: `Department` | Aggregation: `Count`
- **Report 2 (Bar Chart):** `Employees by Location` | Group By: `Location` | Aggregation: `Count`
- **Report 3 (List View):** `Employee List Report` | Columns: `Employee ID`, `Name`, `Email`, `Department`, `Location`

### **Phase 9: Build Executive Dashboard**
- Opened `PA_DASHBOARDS.FORM` (ACL `pa_dashboards` Admin Overrides = True).
- Created Dashboard: `Employee Analytics Dashboards`.
- Embedded all 3 Reports as active widgets.

---

## 📊 Summary Metrics & Verification

| Metric | Initial Load | Delta Load | Re-Run Load |
| :--- | :---: | :---: | :---: |
| **Total Rows Processed** | 15 | 4 | 4 |
| **Records Inserted** | 15 | 2 | 0 |
| **Records Updated** | 0 | 2 | 0 |
| **Records Ignored** | 0 | 0 | 4 |
| **Transform Errors** | 0 | 0 | 0 |
| **Coalesce Key** | `u_employee_id` | `u_employee_id` | `u_employee_id` |

---
*Updated for Team: Moorthy R (Team Lead), Priyan N (Member), KATHIRAVAN M (Member).*
