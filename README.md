# kubepave-tenants

Each tenant is stored as an `XTenant` manifest. The `tenants` Argo CD Application in the management cluster applies it, and Crossplane creates the tenant's Argo CD resources from it.

## Onboard a tenant

Add `local/<tenant-name>/tenant.yaml` and open a pull request. When it is merged, the `tenants` Argo CD Application in the management cluster applies the `XTenant`, and Crossplane creates the tenant's Argo CD resources from it.

## Flow
```
Pull request (adds local/<tenant-name>/tenant.yaml)
        ↓
kubepave-tenants (Git)
        ↓
Argo CD (`tenants` Application, management cluster)
        ↓
Kubernetes (XTenant)
        ↓
Crossplane (`xtenant-gotemplating` Composition)
        ↓
Argo CD (tenant Application + ApplicationSet)
```

## Structure
```
local/<tenant-name>/tenant.yaml
```

Each `tenant.yaml` is an `XTenant`:

```yaml
apiVersion: idp.rezakara.demo/v1beta1
kind: XTenant
metadata:
  name: <tenant-name>
spec:
  shortName: <short-dns-label>
  crossplane:
    compositionRevisionSelector:
      matchLabels:
        channel: stable
```

`metadata.name` must be 3-21 characters and a valid DNS label. `spec.shortName` is at most 10 characters.

## Notes

- Changes go through pull requests
- Each tenant directory represents the desired state for that tenant
- Pruning is on: removing a tenant directory deletes its `XTenant`, and with it the tenant's Argo CD resources and GitHub repo
