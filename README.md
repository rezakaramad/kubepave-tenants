# kubepave-tenants

⚠️ **This file is automatically managed by Crossplane. Do not edit manually.**

This repository contains tenant configurations generated from approved TenantRequests.

Each tenant configuration is stored as a values file and serves as input for Argo CD and Helm to provision and manage tenant infrastructure.

## Flow
```
TenantRequest → Crossplane Function → this repository → Argo CD → Kubernetes resources
```

## Structure
```
tenants/
<tenant-name>/
values.yaml
```

## Notes

- This repository is **managed by the platform (Crossplane)**
- It is continuously updated to reflect the desired state
- Do not modify files manually
- Each tenant directory represents the desired state for that tenant
