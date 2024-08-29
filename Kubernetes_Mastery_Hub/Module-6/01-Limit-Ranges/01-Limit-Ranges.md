# LimitRange

## << --- In Progress --- >>

LimitRanges in Kubernetes provide a way to enforce resource usage policies across pods in a namespace.

## What is LimitRange.?

- LimitRanges in Kubernetes are like setting rules for how much resources (like CPU and memory) each pod in your cluster can use.
- It's a way to make sure that no pod takes too much of the cluster's resources, which could slow down or even crash other pods running on the same cluster.
- So, LimitRanges help keep everything running smoothly by setting limits on how much each pod can use.

### Example

> 1 CPU = 1000 milli CPUs or 1000m

For example, you define a `LimitRange` with this manifest:

```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: cpu-resource-constraint
spec:
  limits:
    - default: # this section defines default limits
        cpu: 500m
      defaultRequest: # this section defines default requests
        cpu: 500m
      max: # max and min define the limit range
        cpu: "1"
      min:
        cpu: 100m
      type: Container
```

along with a Pod that declares a CPU resource request of `700m`, but not a limit:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: example-conflict-with-limitrange-cpu
spec:
  containers:
    - name: demo
      image: registry.k8s.io/pause:2.0
      resources:
        requests:
          cpu: 700m
```

then that Pod will not be scheduled, failing with an error similar to:

```yaml
Pod "example-conflict-with-limitrange-cpu" is invalid: spec.containers[0].resources.requests: Invalid value: "700m": must be less than or equal to cpu limit
```

If you set both `request` and `limit`, then that new Pod will be scheduled successfully even with the same `LimitRange` in place:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: example-no-conflict-with-limitrange-cpu
spec:
  containers:
    - name: demo
      image: registry.k8s.io/pause:2.0
      resources:
        requests:
          cpu: 700m
        limits:
          cpu: 700m
```
