## PowerApps Remittance Writeup

This solution monitors a shared revenue mailbox, automatically captures incoming remittance emails, archives payment files to SharePoint, extracts payment information, and presents the results through a centralized Power Apps dashboard. Solution updates and collaborations are completely contained in a private sandbox/production environment. (There is no Git version control for PowerApps solutions!)

Gio's Notes:
- Set-Up Shared Mailbox Trigger
- Create a compose function to set the parameters for how and when these payments should be recorded
- Create a SharePoint List (The column records that you intend to display - you'll also map these headers back in the Power Automate Flow (Dynamic))
- Create a SharePoint Document Library (you need somewhere to store files so that you can complete your read/write logic before pulling to your list to update your records)
- Add a new Action after your component - connect your site address from SharePoint
- Add an Apply to each trigger w/ Attachments output parameter (and then add a Create File action within that loop w/ the Site Address (Revenue SharePoint and Payment Folder Path

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
Excel Script & Regex
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
*This repository contains no PowerApps solution obviously, it's mainly so that I don't forget this stuff in the future and can look back when needed
