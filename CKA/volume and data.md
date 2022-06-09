# Volume and data

Three access modes:  

- ReadWriteOnce, which allows read-write by a single **node**
- ReadOnlyMany, which allows read-only by multiple nodes
- ReadWriteMany, which allows read-write by many nodes

## Volume spec

- emptyDir  
he kubelet will create the directory in the container, but not mount any storage. Any data created is written to the shared container space. As a result, it would not be persistent storage.

`
kubectl exec -ti busybox -- cat /mysqlpassword/password
`

The name of secret is 'password'.
