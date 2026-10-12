# 📋 ITIL Runbooks & Templates

ITIL-aligned runbooks, change request templates, restore test checklists, and post-incident report templates for IT infrastructure and backup operations.

> 🧪 **Reference / lab project.** Original practice code written to demonstrate the approach. It is not taken from an employer's codebase. Review and adapt before using it in your own environment.

---

## 📁 Repository Structure

```
itil-runbooks-templates/
├── runbooks/
│   └── backup_incident_response.md     # Step-by-step backup failure response
├── templates/
│   ├── change_request_template.md      # ITIL Change Request template
│   └── post_incident_report.md         # Post-Incident Report (PIR) template
├── checklists/
│   └── restore_test_checklist.md       # Restore test validation checklist
└── README.md
```

---

## 📌 When to Use Each Document

| Document | When |
|----------|------|
| Backup Incident Response | Backup job fails or snapshot is missing |
| Change Request Template | Any change to backup config or infrastructure |
| Post-Incident Report | After any P1/P2 backup-related incident |
| Restore Test Checklist | Weekly/monthly restore validation exercises |

---

## 🔄 ITIL Process Overview

```
Incident Detected
      │
      ▼
Incident Logged (Ticketing System)
      │
      ▼
Triage & Severity Classification
      │
      ├──► P1/P2: Immediate escalation + war room
      └──► P3/P4: Standard response queue
              │
              ▼
        Restore / Fix
              │
              ▼
        Incident Closed
              │
              ▼
     Problem Management (recurring?)
              │
              ▼
       Change Request raised
              │
              ▼
       Post-Incident Report
```

---

## 👤 Author

**Manicharan Ravi** — IT Specialist & Cloud Engineer  
📧 manicharan.ravi999@gmail.com  
🔗 [linkedin.com/in/manicharan-ravi](https://linkedin.com/in/manicharan-ravi)
