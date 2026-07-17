## PowerApps Remittance Writeup

This solution monitors a shared revenue mailbox, automatically captures incoming remittance emails, archives payment files to SharePoint, extracts payment information, and presents the results through a centralized Power Apps dashboard. Solution updates and collaborations are completely contained in a private sandbox/production environment. (There is no Git version control for PowerApps solutions!)

---

## Workflow

```text
Shared Mailbox
        │
        ▼
When New Email Arrives
        │
        ▼
Power Automate Trigger
        │
        ▼
Create SharePoint Record
        │
        ▼
Loop Through Attachments
        │
        ▼
Filter Attachment Type
        │
        ▼
Save Excel Workbook
        │
        ▼
Run Office Script
        │
        ├───────────────┐
        ▼               ▼
Company Name     Payment Amount
        │               │
        └───────┬───────┘
                ▼
Update SharePoint Record
                │
                ▼
Attach Original Workbook
                │
                ▼
Power Apps Dashboard
```

---

## Full Project Structure

```text
Kelly Services Remittance Dashboard
├── Power Automate
│   ├── Shared Mailbox Trigger
│   ├── Compose
│   ├── Create SharePoint Record
│   ├── Apply to Each Attachment
│   │   ├── Attachment Filter
│   │   ├── Get Attachment (V2)
│   │   ├── Create File
│   │   ├── Run Office Script
│   │   ├── Add Attachment
│   │   └── Update SharePoint Record
│   └── Error Handling (Future)
│
├── SharePoint
│   ├── Power Platforms Remittance Records
│   └── Remittance Dashboard
│       └── Archived Payment Files
│
├── Office Scripts
│   └── Kelly Payment Parser
│       ├── Company Name Extraction
│       ├── Payment Amount Extraction
│       └── Excel Validation
│
└── Power Apps
    ├── Remittance Dashboard
    ├── Payment Gallery
    ├── Payment Details Panel
    ├── Attachment Viewer
    └── Search & Filtering 
```
*This repository contains no PowerApps solution 
