# Sprint 12 — Velero Backups

| File | What to capture |
|------|----------------|
| `01-velero-backup-list.png` | Terminal: `velero backup get` — backup listed as Completed with timestamp |
| `02-velero-schedule.png` | Terminal: `velero schedule get` — `demo-namespace-daily` schedule Active |
| `03-ebs-snapshot-console.png` | AWS Console → EC2 → Snapshots — snapshot created at backup time |
| `04-velero-s3-bucket.png` | AWS Console → S3 → `pel-velero-dev` — backup objects present |
