# ✅ Restore Test Checklist

**Frequency:** Weekly (critical systems) / Monthly (standard systems)  
**Purpose:** Validate that backups can actually be restored — a backup not tested is not a backup.

---

## Test Details

| Field | Value |
|-------|-------|
| **Test Date** | YYYY-MM-DD |
| **Engineer** | _(name)_ |
| **System Under Test** | _(DB identifier / VM name)_ |
| **Snapshot/Backup Used** | _(ID)_ |
| **Snapshot Age** | _(hours old at time of test)_ |
| **Test Environment** | _(isolated test instance — never production)_ |

---

## Pre-Test Checks

- [ ] Test will be performed on isolated environment (not production)
- [ ] Test instance naming follows convention: `restore-test-YYYYMMDD`
- [ ] Sufficient resources available in test environment
- [ ] Latest snapshot identified and status = `available`
- [ ] Snapshot age is within RPO window
- [ ] Test procedure reviewed and understood

---

## Restore Execution

- [ ] Restore initiated at: `HH:MM UTC`
- [ ] Restore method: _(snapshot restore / PITR / full restore)_
- [ ] Test instance available at: `HH:MM UTC`
- [ ] Total restore time: `_____ minutes`
- [ ] RTO target met: Yes / No (target: _____ minutes)

---

## Data Integrity Checks

- [ ] Connection to restored instance successful
- [ ] Database engine version matches source: _(version)_
- [ ] Schema validation passed (tables/objects present)
- [ ] Row count check: `_____ rows` in key tables
- [ ] Sample query executed successfully
- [ ] Application-level test (if applicable): Pass / Fail / N/A
- [ ] No data corruption errors in logs

---

## Post-Test Cleanup

- [ ] Test instance deleted after validation
- [ ] No test data accessible from production network
- [ ] Test resources fully de-provisioned

---

## Result Summary

| Check | Result | Notes |
|-------|--------|-------|
| Restore completed | ✅ / ❌ | |
| RTO met | ✅ / ❌ | Target: ___ min, Actual: ___ min |
| Data integrity | ✅ / ❌ | |
| RPO confirmed | ✅ / ❌ | Snapshot age: ___ hours |
| **Overall Result** | **PASS / FAIL** | |

---

## Issues Found

_(List any issues discovered during this restore test)_

| Issue | Severity | Action Required |
|-------|----------|----------------|
| | | |

---

## Sign-Off

| Role | Name | Date |
|------|------|------|
| Test Engineer | | |
| Team Lead Review | | |

---

> **Note:** All restore test results must be retained for compliance and audit purposes.  
> Log file location: `/var/log/backup-restore-tests/`
