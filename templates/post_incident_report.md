# 📊 Post-Incident Report (PIR)

> Complete within 48 hours of P1/P2 incident resolution.

---

## Incident Summary

| Field | Value |
|-------|-------|
| **Incident ID** | INC-YYYY-XXX |
| **Title** | _(brief description)_ |
| **Severity** | P1 / P2 |
| **Date/Time Detected** | YYYY-MM-DD HH:MM UTC |
| **Date/Time Resolved** | YYYY-MM-DD HH:MM UTC |
| **Total Duration** | _(hours/minutes)_ |
| **Data Loss Window** | _(time between last good backup and incident)_ |
| **Systems Affected** | _(list)_ |
| **Report Author** | _(name)_ |
| **Report Date** | YYYY-MM-DD |

---

## 1. Incident Timeline

| Time (UTC) | Event |
|------------|-------|
| HH:MM | Alert triggered in monitoring system |
| HH:MM | On-call engineer acknowledged |
| HH:MM | Incident ticket created |
| HH:MM | Root cause identified |
| HH:MM | Restore/fix initiated |
| HH:MM | Service restored |
| HH:MM | Validation completed |
| HH:MM | Incident closed |

---

## 2. Root Cause Analysis

**Root Cause:**
> _(What was the underlying technical cause? Be specific.)_

**Contributing Factors:**
- _(factor 1)_
- _(factor 2)_

**Why was it not detected earlier?**
> _(Gap in monitoring, alerting, or process)_

---

## 3. Impact Assessment

| Category | Impact |
|----------|--------|
| Data loss | _(none / X hours / X GB)_ |
| Service downtime | _(none / X minutes)_ |
| Users affected | _(number)_ |
| Business impact | _(low / medium / high)_ |
| SLA breached | Yes / No |

---

## 4. Resolution Actions Taken

1. _(action 1)_
2. _(action 2)_
3. _(action 3)_

---

## 5. Preventive Actions (Action Items)

| # | Action | Owner | Due Date | Status |
|---|--------|-------|----------|--------|
| 1 | _(action)_ | _(name)_ | YYYY-MM-DD | Open |
| 2 | _(action)_ | _(name)_ | YYYY-MM-DD | Open |
| 3 | _(action)_ | _(name)_ | YYYY-MM-DD | Open |

---

## 6. Lessons Learned

**What went well:**
- _(e.g., quick detection via CloudWatch alerts)_

**What could be improved:**
- _(e.g., runbook was outdated)_

**Process changes recommended:**
- _(e.g., add snapshot integrity check to daily routine)_

---

## 7. Sign-Off

| Role | Name | Date |
|------|------|------|
| Incident Owner | | |
| Team Lead | | |
| Problem Manager | | |
