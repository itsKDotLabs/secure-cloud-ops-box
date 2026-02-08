## Role Name
ec2-secure-ops-ssm-role

## Purpose
Provides IAM-based, least privilege access for managing a hardened EC2
operations host exclusively via AWS Systems Manager Session Manager.

## Key Design Decisions
- No static credentials
- No SSH key pairs
- Access mediated through IAM + SSM
- Role scoped to instance-level operations only
