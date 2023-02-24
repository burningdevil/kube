# ServiceAccount

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
 name: backend-sa #修改 name
 namespace: qa #注意添加 namespace
automountServiceAccountToken: false #修改为 false，表示不自动挂载 secret
```

```yaml
创建 Pod 使用该 ServiceAccount
vi /cks/sa/pod1.yaml
修改如下内容
……
metadata:
 name: backend
 namespace: qa #注意命名空间是否对
spec:
 serviceAccountName: backend-sa # 没有则添加一行，有则修改这一行为刚才创建的 ServiceAccount（考试时，默认已有这一行，需要修改。）
 containers:
……
```
