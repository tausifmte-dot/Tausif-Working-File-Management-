# CRM System — Security Implementation Checklist

## Phase 1: IMMEDIATE (Week 1)

### Master Password & Authentication
- [ ] Master password set to strong value (12+ chars, mixed case, numbers, symbols)
- [ ] Test master password reset functionality
- [ ] Document master password in secure password manager (NOT in plain text)
- [ ] Each team member has unique master password
- [ ] Session timeout configured (30 minutes)
- [ ] Test auto-logout on browser close
- [ ] Verify `sessionStorage` unlock flag (`crm_unlocked`) is cleared on tab close
- [ ] Confirm SHA-256 password hash (`_shx` + salt) is NOT committed to any public repo

### GitHub Configuration
- [ ] GitHub account created with 2FA enabled
- [ ] Private repository created (`crm-data`)
- [ ] Personal Access Token generated (repo scope ONLY)
- [ ] GitHub PAT stored in system Settings (localStorage key: `crm_gh_token`)
- [ ] Branch protection enabled on `main`
- [ ] Require signed commits configured
- [ ] Test sync (Settings → GitHub Sync → Save & Test Connection)
- [ ] Verify sync file target is `crm-data.json` on branch `main`

### Device Security
- [ ] Full disk encryption enabled (BitLocker/FileVault/LUKS)
- [ ] Antivirus/anti-malware installed
- [ ] Latest OS security updates applied
- [ ] Firewall enabled
- [ ] Screen lock timeout set to 5 minutes

### Access Control
- [ ] Only authorized team members have access
- [ ] Admin account created for system management
- [ ] Non-admin user account created for daily use
- [ ] Master password NOT shared among users
- [ ] Initial backup created and stored securely

---

## Phase 2: SHORT-TERM (Weeks 2-4)

### Audit Logging
- [ ] Audit log functionality tested (localStorage key: `crm_log`)
- [ ] Failed login attempts logged
- [ ] Data modifications logged with timestamp
- [ ] Export actions logged (PDF / JSON / DOCX)
- [ ] Review audit logs for first week of operation
- [ ] Document any unusual activity

### Data Protection
- [ ] Sensitive client fields identified (phone, email, financial info, contact history)
- [ ] Data classification completed
- [ ] Client PII masking in UI configured
- [ ] Phone numbers verified format
- [ ] Test any external integrations (email, messaging) for data-leak safety
- [ ] Confirm client data (localStorage key: `crm_data`) is only stored locally + private GitHub repo

### Backup & Recovery
- [ ] Initial automated GitHub sync working
- [ ] Manual JSON export tested
- [ ] Backup stored on external encrypted drive
- [ ] Backup verification checklist completed
- [ ] Restore procedure documented

### Documentation
- [ ] Security policy distributed to all users
- [ ] Users acknowledge receipt of policy
- [ ] Incident response procedure documented
- [ ] Disaster recovery plan created
- [ ] Security contacts list shared with team

---

## Phase 3: ONGOING (Monthly)

### Access Review
- [ ] Monthly audit of user access
- [ ] Inactive users removed
- [ ] GitHub collaborators reviewed
- [ ] Admin permissions verified (least privilege)
- [ ] Document access review

### Security Monitoring
- [ ] Review audit logs for suspicious activity
- [ ] Check GitHub security alerts
- [ ] Verify backup integrity
- [ ] Monitor for failed login attempts
- [ ] Test incident response procedure

### Maintenance
- [ ] Update browser to latest version
- [ ] Update OS security patches
- [ ] Run antivirus full scan
- [ ] Verify device encryption status
- [ ] Update password manager
- [ ] Review third-party CDN libraries used by the app (jsPDF, Chart.js, docx) for known CVEs

### Compliance
- [ ] Verify data retention policies followed
- [ ] Check for client records older than retention period
- [ ] Confirm backups still accessible
- [ ] Review any privacy policy changes
- [ ] Document compliance check

---

## Phase 4: QUARTERLY (Every 3 Months)

### Password Rotation
- [ ] Master password changed (if no recent change) — regenerate SHA-256 hash + salt in `_rAsm()` / `_rHsh()`
- [ ] GitHub PAT rotated (every 6 months)
- [ ] Other service passwords updated
- [ ] Old passwords documented in secure location
- [ ] Update security contacts

### Disaster Recovery Testing
- [ ] Test restore from GitHub backup (`crm-data.json`)
- [ ] Test restore from external backup
- [ ] Verify all client data restored correctly
- [ ] Document restore time
- [ ] Update recovery procedure if needed

### Security Audit
- [ ] Review full audit log (last 3 months)
- [ ] Investigate any anomalies
- [ ] Review security incidents (if any)
- [ ] Update incident response procedures
- [ ] Share findings with team

### Policy Review
- [ ] Review security policy for updates
- [ ] Update threats/risks assessment
- [ ] Adjust policies if needed
- [ ] Communicate changes to users
- [ ] Document review in change log

---

## Phase 5: ANNUALLY (Once per Year)

### Security Training
- [ ] All users complete security training
- [ ] Phishing simulation testing
- [ ] Password security refresh
- [ ] Client data protection training
- [ ] Incident response drill

### Vulnerability Assessment
- [ ] Check for known vulnerabilities in dependencies (jsPDF, jspdf-autotable, Chart.js, docx.js)
- [ ] Review code for security issues (XSS via client name/notes fields, localStorage handling)
- [ ] Penetration testing (if budget allows)
- [ ] Document findings
- [ ] Create remediation plan

### Certificate & License Review
- [ ] Verify GitHub account still active
- [ ] Check domain registration (if applicable)
- [ ] Review software licenses compliance
- [ ] Update certificates if needed
- [ ] Document expiration dates

### Full Security Review
- [ ] Comprehensive security audit
- [ ] Risk assessment update
- [ ] Threat model review
- [ ] Controls effectiveness evaluation
- [ ] Security metrics analysis

---

## Security Incident Response Checklist

### When Incident Occurs

**IMMEDIATE (First Hour)**
- [ ] Stop further access to the system
- [ ] Notify Security Officer immediately
- [ ] Preserve all logs and evidence (export `crm_log` before wiping)
- [ ] Assess scope: How many client records affected?
- [ ] Assess severity: Critical/High/Medium/Low?

**URGENT (Next 24 Hours)**
- [ ] Take system offline if critical breach
- [ ] Backup all current data
- [ ] Reset master password for all users (rotate `_rHsh()` hash value)
- [ ] Revoke GitHub PAT
- [ ] Review audit logs for unauthorized access
- [ ] Notify affected clients
- [ ] Document incident details
- [ ] Begin root cause analysis

**FOLLOW-UP (Within 7 Days)**
- [ ] Complete incident investigation
- [ ] Identify how breach occurred
- [ ] Implement immediate fixes
- [ ] Update security policies
- [ ] Communicate findings to team
- [ ] Test system thoroughly before resuming
- [ ] Document lessons learned

---

## GitHub Security Hardening

### Essential Setup
- [ ] Repository visibility: PRIVATE ✓ (`crm-data`)
- [ ] Require pull request reviews: YES ✓
- [ ] Minimum number of approvals: 1 ✓
- [ ] Require status checks: YES ✓
- [ ] Require branches up to date: YES ✓
- [ ] Allow force pushes: NO ✓
- [ ] Allow deletions: NO ✓
- [ ] Require signed commits: YES ✓

### Access Management
- [ ] Collaborators reviewed
- [ ] Each user has least privilege needed
- [ ] Admin role restricted to 1-2 people
- [ ] Inactive users removed
- [ ] GitHub 2FA enabled for all
- [ ] SSH keys up to date
- [ ] Deploy keys used (not personal keys)

### Monitoring
- [ ] Security alerts enabled
- [ ] Vulnerable dependencies flagged
- [ ] Commit logs reviewed weekly
- [ ] Access logs reviewed monthly
- [ ] Unusual activity investigated

---

## User Onboarding Checklist

### When New Team Member Joins

**Before First Access**
- [ ] Read and sign security policy
- [ ] Complete security training
- [ ] Create strong master password
- [ ] Setup password manager account
- [ ] Device security hardening checklist
- [ ] Test system access

**First Day**
- [ ] Master password verified
- [ ] System orientation completed (Dashboard, Clients, Analytics, Settings)
- [ ] Practice logout/login
- [ ] Review client data classification
- [ ] Understand incident reporting
- [ ] Know security contacts

**Ongoing**
- [ ] Monthly security check-in
- [ ] Reinforce security practices
- [ ] Address any concerns
- [ ] Update contact information

---

## User Offboarding Checklist

### When Team Member Leaves

**Before Final Day**
- [ ] Schedule handover meeting
- [ ] Document all data access
- [ ] Create backup of their work
- [ ] Note any pending tasks

**Final Day**
- [ ] Change master password
- [ ] Remove GitHub access
- [ ] Revoke GitHub PAT (if they had one)
- [ ] Disable account access
- [ ] Collect any devices

**After Final Day**
- [ ] Verify access removed
- [ ] Archive their audit logs
- [ ] Review for any outstanding issues
- [ ] Confirm no data remains on removed device
- [ ] Document termination

---

## Critical Security Contacts

Keep this information accessible but SECURE:

