When using `vars:`, I can't get the value of the vars for `commonLabels` nor `nameSuffix`.

Run:

```shell
kustomize build overlays/dev/
```

Actual output:

```yaml
apiVersion: v1
data:
  MY_VAR: my-merged-value
kind: ConfigMap
metadata:
  labels:
    my-var-label: my-merged-value
    non-var-label: non-var
  name: my-config-$(MY_VAR)-5hd24f6279
---
apiVersion: v1
kind: Pod
metadata:
  labels:
    my-var-label: my-merged-value
    name: busybox
    non-var-label: non-var
  name: busybox-$(MY_VAR)
spec:
  containers:
  - image: busybox:$(MY_VAR)
    name: busybox

```

Expected output:

```yaml
apiVersion: v1
data:
  MY_VAR: my-merged-value
kind: ConfigMap
metadata:
  labels:
    my-var-label: my-merged-value
    non-var-label: non-var
  name: my-config-my-merged-value-5hd24f6279
---
apiVersion: v1
kind: Pod
metadata:
  labels:
    my-var-label: my-merged-value
    name: busybox
    non-var-label: non-var
  name: busybox-my-merged-value
spec:
  containers:
  - image: busybox:my-merged-value
    name: busybox


```
