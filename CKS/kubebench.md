# Kubebench

## What is CIS

This CIS Benchmark is the product of a community consensus process and consists of secure configuration guidelines developed for Kubernetes.

## Kube-bench

kube-bench is a tool that checks whether Kubernetes is deployed securely by running the checks documented in the CIS Kubernetes Benchmark.

## Usage

`kube-bench run --check $version`

result:

```none
[INFO] 1.2 API Server
[FAIL] 1.2.20 Ensure that the --profiling argument is set to false (Automated)

== Remediations master ==
1.2.20 Edit the API server pod specification file /etc/kubernetes/manifests/kube-apiserver.yaml
on the master node and set the below parameter.
--profiling=false


== Summary master ==
0 checks PASS
1 checks FAIL
0 checks WARN
0 checks INFO

[INFO] 2 Etcd Node Configuration

== Summary etcd ==
0 checks PASS
0 checks FAIL
0 checks WARN
0 checks INFO

[INFO] 3 Control Plane Configuration

== Summary controlplane ==
0 checks PASS
0 checks FAIL
0 checks WARN
0 checks INFO

[INFO] 4 Worker Node Security Configuration

== Summary node ==
0 checks PASS
0 checks FAIL
0 checks WARN
0 checks INFO

[INFO] 5 Kubernetes Policies

== Summary policies ==
0 checks PASS
0 checks FAIL
0 checks WARN
0 checks INFO

== Summary total ==
0 checks PASS
1 checks FAIL
0 checks WARN
0 checks INFO
```
