# Kong

# Trivia:

## Kong or Nginx ingress cannot access it's configmap

### Cause:

`--ingress-class` was set differently, led to:

- ConfigMap is missing.
- RBAC was not found.

### Detail:

It's happen when you find something like this:

```
E0306 18:59:18.057699       1 leaderelection.go:324] error retrieving resource lock kong/something-kong: configmaps "something-kong" is forbidden: User "system:serviceaccount:kong:kong-serviceaccount " cannot get resource "configmaps" in API group "" in the namespace "kong"
E0306 18:59:27.653349       1 leaderelection.go:324] error retrieving resource lock kong/something-kong: configmaps "something-kong" is forbidden: User "system:serviceaccount:kong:kong-serviceaccount " cannot get resource "configmaps" in API group "" in the namespace "kong"
```

### Solution:

when you change `ingress-class`, make sure to:

- Create new `ConfigMaps`
- Create new `ClusterRole`
- Create new `ClusterRoleBinding`

with correct name

please see: kong's `deploy/single/all-in-one-postgres.yaml` file for detail.

---
