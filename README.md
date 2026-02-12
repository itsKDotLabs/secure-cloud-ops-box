# Secure Cloud Ops Box

A hardened AWS EC2 Ubuntu instance designed to practice secure cloud operations using
IAM-based access, zero inbound network exposure, and host-level visibility.

---

## Objectives

- Eliminate SSH-based access
- Enforce least-privilege IAM
- Harden Linux host controls
- Increase persistence & privilege visibility
- Implement cloud-native artifact workflow
- Document real-world security decisions

---

## Threat Model

This project assumes a realistic cloud threat landscape:

- Credential compromise
- Management plane exposure
- Privilege escalation
- Persistence mechanisms

Focus is placed on understanding attacker behaviors and improving defensive visibility.

---

## Security Design Decisions

- SSH access eliminated; management performed exclusively via AWS Systems Manager (SSM)
- EC2 instance configured with zero inbound security group rules
- IAM role used instead of static credentials
- Privilege escalation visibility enhanced via dedicated sudo logging
- Kernel-level auditing enabled via auditd
- Detection-focused visibility implemented across persistence and privilege escalation surfaces

---

## Architecture

Management Plane:

User → AWS Console / CLI → SSM Session Manager → EC2 Instance

Telemetry Pipeline (Next Phase):

Host Logs → CloudWatch Logs → Detection & Alerting

(see diagrams/)

---

## Evidence & Artifacts

Artifacts are generated directly on the EC2 host via AWS Systems Manager Session Manager,
stored in a private S3 bucket, then retrieved using AWS CLI.

Phase 2 validation artifacts:

- `logs/phase2-auditctl-rules.txt`  
  Active auditd rules confirming monitoring coverage

- `logs/phase2-ausearch-cron-persistence.txt`  
  Validation of cron-based persistence monitoring

- `logs/phase2-ausearch-sudoers-change.txt`  
  Validation of privilege escalation visibility

---

## Monitoring & Visibility Focus

Monitoring is implemented across high-risk persistence and escalation surfaces,
including:

- sudo policy modifications
- identity store changes
- cron task monitoring
- shell initialization files
- SSH key activity
- systemd service directories
- PATH-sensitive directories

This project prioritizes understanding attacker mechanisms and defensive visibility.

---

## Key Lessons Learned

- Eliminating SSH significantly reduces attack surface
- auditd requires strict path accuracy and existence validation
- sudo does not apply to shell redirection operations
- Persistence mechanisms are often simpler than expected
- Cloud-native artifact workflows improve operational consistency

---

## Future Enhancements

- Centralized log shipping via CloudWatch Agent
- Detection alerting & metric filters
- Automated baseline validation scripts
- Expanded persistence monitoring coverage
- Infrastructure-as-Code (IaC) deployment model

---

## Closing Notes

This project is intentionally designed to reflect practical cloud security engineering:

Visibility over assumptions  
Detection over tooling  
Mechanisms over artifacts