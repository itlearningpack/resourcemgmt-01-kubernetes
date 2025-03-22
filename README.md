# Exceed a Container's memory limit  

A Container can exceed its memory request if the Node has memory available. But a Container is not allowed to use more than its memory limit. If a Container allocates more memory than its limit, the Container becomes a candidate for termination. If the Container continues to consume memory beyond its limit, the Container is terminated. If a terminated Container can be restarted, the kubelet restarts it, as with any other type of runtime failure.

In this exercise, you create a Pod that attempts to allocate more memory than its limit. Here is the configuration file for a Pod that has one Container with a memory request of 50 MiB and a memory limit of 250 MiB:

### Pod Configuration for Liveness HTTP-GET

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: resourcemgmt1
  labels:
   app: v1.0.0
spec:
  containers:
  - name: resourcemgmt1
    image: docker.io/polinux/stress:latest
    imagePullPolicy: IfNotPresent
    resources:
      requests:
        memory: "50Mi"
      limits:
        memory: "250Mi"
    command: ["stress"]
    args: ["--vm", "1", "--vm-bytes", "150M", "--vm-hang", "1"]

```
