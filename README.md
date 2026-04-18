# kubepave-tenants

⚠️ **This repository is managed by Crossplane. Do not edit manually.**

This repository contains tenant configurations generated from approved TenantRequests.

Each tenant configuration is stored as a values file and serves as input for Argo CD and Helm to provision and manage tenant infrastructure.

## Flow
```
kubepave-tenant-requests (Git)
        ↓
Argo CD
        ↓
Kubernetes (TenantRequest)
        ↓
Crossplane Function
  - Validate
        ↓
Approval Gate (manual or automated)
        ↓
Crossplane Function
  - Generate tenant configuration
  - Push to kubepave-tenants repository
        ↓
kubepave-tenants (Git)
        ↓
Argo CD
        ↓
Helm (rendering)
        ↓
Kubernetes (Tenant resources)
```

## Structure
```
tenants/<tenant-name>/tenant.yaml
```

## Notes

- This repository is **managed by the platform (Crossplane)**
- It is continuously updated to reflect the desired state
- Do not modify files manually
- Each tenant directory represents the desired state for that tenant
