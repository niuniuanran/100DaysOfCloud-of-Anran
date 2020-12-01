# RDS
- backed by EBS (gp2 or io1)
- You cannot SSH into your RDS instance

## RDS Backups
### Automated backups
- automatically enabled
- daily full backup
- transaction logs every 5 mins
- 7 day retention by default, up to 35 days.

### Snapshots
- Mannually triggered by user
- Retention for as long as you want

## RDS Read Replicas
- read replica can be same AZ, cross AZ, cross region
- 