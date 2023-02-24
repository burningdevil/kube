# RuntimeClass

```yaml
1 创建 RuntimeClass
vi /cks/gVisor/rc.yaml
修改或添加如下内容
apiVersion: node.k8s.io/v1 ##将 apiVersion: node.k8s.io/v1beta1 修改为 apiVersion: node.k8s.io/v1。这个在 1.25 正式考试的时候，是对的，不需要修改的。
kind: RuntimeClass
metadata:
 name: untrusted # 用来引用 RuntimeClass 的名字，RuntimeClass 是一个集群层面的资源
handler: runsc # 对应的 CRI 配置的名称
创建
kubectl create -f /cks/gVisor/rc.yaml
```

```yaml
 spec: #找到这个 spec，注意在 deployment 里是有两个单独行的 spec 的，要找第二个，也就是下面有 containers 这个字段的 spec。
 runtimeClassName: untrusted #添加这一行，注意空格对齐，保存会报错，忽略即可。
 containers:
 - image: nginx:1.9
 imagePullPolicy: IfNotPresent
 name: run-test
```
