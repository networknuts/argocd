Multi-document Kubernetes manifest covering the entire deployment lifecycle:

1. PreSync Hook: A Kubernetes Job that runs nginx -t using the official Alpine Nginx image to validate syntax before deployment.

2. Main Application: A standard 3-replica Nginx deployment exposed via a ClusterIP service on port 80.

3. PostSync Hook: A temporary Job running a lightweight curl loop against the internal nginx-service DNS entry.

4. SyncFail Hook (nginx-sync-fail-notification): A dedicated Kubernetes Job that executes only if any prior step fails. It simulates sending a failure alert (e.g., Slack, PagerDuty, or Webhook) with application metadata. It uses the BeforeHookCreation delete policy to ensure that subsequent deployment attempts clean up old failure job resources before running again.

