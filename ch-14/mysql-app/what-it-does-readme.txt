1. PreSync Hook (mysql-pre-backup): Runs a temporary Kubernetes Job to export a fast backup (mysqldump) of your current data before applying changes.

2. Main Application: Standard persistent infrastructure consisting of a Kubernetes Secret for passwords, a PersistentVolumeClaim (PVC) for disk durability, a Deployment running MySQL 8.0, and a ClusterIP Service.

3. PostSync Hook (mysql-postsync-validation): Probes the live engine to verify database availability and confirms the target database/tables exist and are responsive.

4. SyncFail Hook (mysql-sync-fail-alert): Dynamically triggers an alert if the migration, backup, or deployment fails, pulling a target notification webhook securely from a secret.

