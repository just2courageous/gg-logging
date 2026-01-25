# gg-logging

Centralized Kubernetes logging on **Amazon EKS** using **Fluent Bit** → **CloudWatch Logs**, secured with **IRSA** (pods assume an IAM role, no static keys).

---

## ✅ What this does
- Deploys **Fluent Bit** as a **DaemonSet** in the `logging` namespace
- Tails container logs from `/var/log/containers/*.log`
- Adds Kubernetes metadata (namespace, pod, container)
- Ships logs to **CloudWatch Logs** in **us-east-2**
- Uses **IRSA** so Fluent Bit can write logs without AWS access keys in the cluster

---

## 🧠 Where logs go (current config)
Configured in: `cloudwatch/fluentbit-configmap.yaml`

- **Region:** `us-east-2`
- **Log group:** `/aws/containerinsights/green-guard-gg-eks/application`
- **Stream prefix:** `from-fluent-bit-`

If you want a different log group name, edit:
```conf
log_group_name  /aws/containerinsights/green-guard-gg-eks/application
