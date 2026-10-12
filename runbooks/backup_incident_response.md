# 🚨 Backup Incident Response Runbook

**Version:** 1.2  
**Last Updated:** 2025-03-01  
**Owner:** IT Infrastructure Team  
**Review Cycle:** Quarterly

---

## 1. Purpose

This runbook provides step-by-step procedures for responding to backup failures, missing snapshots, and related incidents. It ensures consistent, ITIL-aligned incident handling with minimal data loss and recovery time.

---

## 2. Severity Classification

| Severity | Condition | Response Time | Escalation |
|----------|-----------|---------------|------------|
| **P1 — Critical** | Production DB backup missing >24h | Immediate | Team Lead + Management |
| **P2 — High** | Backup job failed, last snapshot <24h | Within 1 hour | Team Lead |
| **P3 — Medium** | Non-production backup failed | Within 4 hours | Assigned engineer |
| **P4 — Low** | Warning alerts, no data loss risk | Within 1 business day | Self-managed |

---

## 3. Initial Response Steps

### Step 1 — Acknowledge & Log
- [ ] Acknowledge alert in monitoring system (CloudWatch / Zabbix / PRTG)
- [ ] Create incident ticket in JIRA / ServiceNow
- [ ] Record: time detected, systems affected, initial symptoms

### Step 2 — Assess Scope
```bash
# Check backup job status in AWS Backup
aws backup list-backup-jobs \
  --by-state FAILED \
  --region eu-central-1

# Check RDS snapshots
aws rds describe-db-snapshots \
  --db-instance-identifier <db-id> \
  --query "DBSnapshots[?Status!='available']"

# Check Azure Backup (PowerShell)
Get-AzRecoveryServicesBackupJob -Status Failed
```

### Step 3 — Determine Last Good Backup
```bash
# AWS — find latest available snapshot
aws rds describe-db-snapshots \
  --db-instance-identifier <db-id> \
  --query "reverse(sort_by(DBSnapshots[?Status=='available'], &SnapshotCreateTime))[0]"
```

- [ ] Record last known good backup timestamp
- [ ] Calculate data loss window (current time − last good backup)
- [ ] Communicate data loss window to stakeholders immediately if >1 hour

### Step 4 — Notify Stakeholders
- [ ] Notify team lead (P1/P2 always, P3 if >4 hours)
- [ ] Update incident ticket with initial assessment
- [ ] Set expected resolution time (ETA)

---

## 4. Common Failure Scenarios & Fixes

### 4.1 AWS RDS Snapshot Failed

**Symptoms:** Snapshot status = `failed`, missing from list

**Checks:**
```bash
# Verify RDS instance status
aws rds describe-db-instances \
  --db-instance-identifier <db-id> \
  --query "DBInstances[0].DBInstanceStatus"

# Check CloudWatch logs for errors
aws logs filter-log-events \
  --log-group-name /aws/rds/instance/<db-id>/error \
  --start-time $(date -d '2 hours ago' +%s000)
```

**Common causes & fixes:**
| Cause | Fix |
|-------|-----|
| Insufficient storage | Increase storage or delete old snapshots |
| RDS instance in bad state | Wait for recovery or contact AWS support |
| Snapshot quota exceeded | Delete old manual snapshots |
| IAM permission issue | Verify backup role has `rds:CreateDBSnapshot` |

**Trigger manual snapshot:**
```bash
aws rds create-db-snapshot \
  --db-instance-identifier <db-id> \
  --db-snapshot-identifier manual-recovery-$(date +%Y%m%d%H%M)
```

---

### 4.2 Azure Backup Job Failed

**Symptoms:** Backup job shows error in Recovery Services Vault

**Checks (PowerShell):**
```powershell
# List failed jobs in last 24 hours
$vault = Get-AzRecoveryServicesVault -Name "backup-vault"
Set-AzRecoveryServicesVaultContext -Vault $vault
Get-AzRecoveryServicesBackupJob -Status Failed -From (Get-Date).AddDays(-1)
```

**Common causes & fixes:**
| Error Code | Cause | Fix |
|------------|-------|-----|
| `UserErrorVmNotInDesiredState` | VM stopped/deallocated | Start VM before backup |
| `BackupOperationFailed` | Agent issue | Reinstall Azure Backup agent |
| `StorageAccountNotFound` | Storage config error | Verify vault storage settings |

---

### 4.3 Veeam Backup Job Failed

**Checks:**
1. Open Veeam Backup & Replication console
2. Navigate to **Home → Last 24 hours → Jobs**
3. Check job log for error message
4. Review proxy server availability

**Common fixes:**
| Error | Fix |
|-------|-----|
| Repository full | Free space or add repository |
| Transport error | Restart Veeam Transport Service on target |
| VSS error | Check VSS writer status on VM |
| Proxy unavailable | Verify proxy server is running |

```powershell
# Restart Veeam services if needed
Restart-Service -Name "VeeamBackupSvc"
Restart-Service -Name "VeeamTransportSvc"
```

---

## 5. Escalation Matrix

| Who | When to Escalate | Contact |
|-----|-----------------|---------|
| On-call Engineer | Any P1/P2 alert | Pager / On-call rotation |
| Team Lead | P1 or unresolved P2 >1h | Direct message |
| DBA | Database restore required | DBA on-call |
| Cloud Provider Support | AWS/Azure service issue | Support ticket |
| Management | Customer data at risk | Immediate phone call |

---

## 6. Incident Closure

- [ ] Verify backup is running successfully
- [ ] Confirm restore test on recovered data
- [ ] Update incident ticket with resolution details
- [ ] If recurring → create Problem ticket
- [ ] If config changed → raise Change Request
- [ ] Complete Post-Incident Report (P1/P2 mandatory)

---

## 7. Related Documents

- [Restore Procedure Runbook](./restore_procedure.md)
- [Change Request Template](../templates/change_request_template.md)
- [Post-Incident Report Template](../templates/post_incident_report.md)
- [Restore Test Checklist](../checklists/restore_test_checklist.md)
