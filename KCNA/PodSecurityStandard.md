# Pod Security Standard

The Pod Security Standards define three different policies to broadly cover the security spectrum. These policies are cumulative and range from highly-permissive to highly-restrictive. This guide outlines the requirements of each policy.

- Privileged: Unrestricted policy, providing the widest possible level of permissions. This policy allows for known privilege escalations.
- Baseline: Minimally restrictive policy which prevents known privilege escalations. Allows the default (minimally specified) Pod configuration.
- Restricted: Heavily restricted policy, following current Pod hardening best practices.

## How

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: my-privileged-namespace
  labels:
    pod-security.kubernetes.io/enforce: privileged
    pod-security.kubernetes.io/enforce-version: latest
```

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: my-baseline-namespace
  labels:
    pod-security.kubernetes.io/enforce: baseline
    pod-security.kubernetes.io/enforce-version: latest
    pod-security.kubernetes.io/warn: baseline
    pod-security.kubernetes.io/warn-version: latest
```