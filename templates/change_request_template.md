# 📝 Change Request Template

> Copy this template for every infrastructure or backup configuration change.

---

## CR Header

| Field | Value |
|-------|-------|
| **CR Number** | CR-YYYY-XXX |
| **Title** | _(short description of change)_ |
| **Requestor** | _(name)_ |
| **Date Submitted** | YYYY-MM-DD |
| **Planned Date** | YYYY-MM-DD HH:MM UTC |
| **Change Type** | Standard / Normal / Emergency |
| **Priority** | Low / Medium / High / Critical |
| **Status** | Draft / Pending Approval / Approved / Implemented / Closed |

---

## 1. Description of Change

> What exactly will be changed? Be specific.

_Example: Update AWS Backup lifecycle policy for prod-db from 14-day to 30-day retention._

---

## 2. Business Justification

> Why is this change needed?

_Example: Current 14-day retention does not meet compliance requirement of 30-day data availability._

---

## 3. Scope & Impact

**Systems affected:**
- [ ] Production
- [ ] Staging
- [ ] Development
- [ ] DR Environment

**Services affected:**
- _(list services / databases / applications)_

**Users affected:**
- _(number and type of users impacted)_

**Estimated downtime:** `None / X minutes`

---

## 4. Implementation Plan

| Step | Action | Owner | Duration |
|------|--------|-------|---------|
| 1 | Pre-change backup verification | Engineer | 10 min |
| 2 | _(step)_ | _(owner)_ | _(time)_ |
| 3 | _(step)_ | _(owner)_ | _(time)_ |
| 4 | Post-change validation | Engineer | 15 min |
| 5 | Update documentation | Engineer | 10 min |

---

## 5. Rollback Plan

> How to undo this change if it fails?

_Example: Revert Terraform state to previous version using `terraform apply` with previous `.tfstate`._

**Rollback decision time:** _(how long to attempt before rolling back)_  
**Rollback owner:** _(name)_

---

## 6. Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| _(risk 1)_ | Low/Med/High | Low/Med/High | _(mitigation)_ |
| _(risk 2)_ | Low/Med/High | Low/Med/High | _(mitigation)_ |

**Overall risk level:** 🟢 Low / 🟡 Medium / 🔴 High

---

## 7. Pre-Change Checklist

- [ ] Backup taken before change
- [ ] Rollback plan documented and tested
- [ ] Stakeholders notified
- [ ] Maintenance window scheduled
- [ ] Approval received from Team Lead
- [ ] Change logged in CMDB

---

## 8. Post-Change Validation

- [ ] Change implemented as planned
- [ ] Functionality verified (backup job ran successfully)
- [ ] Monitoring alerts confirmed active
- [ ] Documentation updated
- [ ] Ticket closed

---

## 9. Approvals

| Role | Name | Signature | Date |
|------|------|-----------|------|
| Requestor | | | |
| Team Lead | | | |
| Change Manager | | | |

---

## 10. Change Log

| Date | Author | Description |
|------|--------|-------------|
| YYYY-MM-DD | _(name)_ | Initial draft |
