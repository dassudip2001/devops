# 4.1.2. Rolling Updates and Rollbacks

## I. Rolling Update Strategy

### 1. What is a Rolling Update?

- Rolling Updates in Deployments is a strategy for updating your application without causing downtime.
- It allows you to gradually replace old instances of your application with new ones.

### 2. Why Use Rolling Updates?

- **Zero Downtime**: Ensures that the application remains available throughout the update process.
- **Smooth Transition**: Gradually introduces changes, reducing the risk of introducing errors or downtime.

### 3. How Rolling Update Works?

- Kubernetes creates new Pods with the updated configuration while terminating the old Pods.
- The process continues until all old Pods are replaced with new ones.

#### 3.1 What k8s dose behind to achive Rolling Update?

- Kubernetes creats a new `ReplicaSet` with the updated pod template while gradually scaling down the old `ReplicaSet`.

### 4. Rolling Update configuration inside Deployment YAML file

- It should be under `spec.stratergy`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app-deployment
spec:
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 1
      maxSurge: 1
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-app-container
          image: my-app-image:v2
```

In this example:

- **maxUnavailable: 1**: Specifies that at most one Pod can be unavailable during the update.
- **maxSurge: 1**: Specifies that at most one additional Pod can be created above the desired number of replicas during the update.

#### **MaxUnavailable & MaxSurge**

- **maxUnavailable**: Controls the maximum number of Pods that can be unavailable during the update. If set to `1`, it means that one Pod can be taken down while the new one is brought up.
- **maxSurge**: Controls the maximum number of extra Pods that can be created beyond the desired number of replicas during the update. If set to `1`, it allows one extra Pod to be created temporarily during the update process.

**Example**:

- If you have a Deployment with `3` replicas and you set `maxUnavailable` to `1` and `maxSurge` to `1`, during the Rolling Update, Kubernetes might have up to `4` Pods running temporarily, but never fewer than `2`.

---

## II. Rollbacks in Deployments

- Lets say, your update doesn't go as planned.
- Rollbacks allows you to revert to a previous working version.
- Kubernetes keeps track of the Deployment's revision history, allowing you to easily roll back to a stable version.

### **Steps to perform a Rollback**

#### **1.** View Deployment History to identify the desired revision you want to rollback to:

```bash
kubectl rollout history deployment my-deployment
```

#### **2.** Rollback to previous state or last state

```bash
kubectl rollout undo deployment my-deployment
```

#### **3.** Rollback to a Specific Revision, Eg:- roll back to revision 2

```bash
kubectl rollout undo deployment my-deployment --to-revision=2
```

#### **4.** Monitor Rollback:

```bash
kubectl rollout status deployment my-deployment
```

#### **5.** Confirm Rollback:

```bash
kubectl get deployment
```

---

## Versioning:

Kubernetes automatically assigns a revision number to each update made to a Deployment. This versioning helps in tracking the changes and rolling back to specific versions if needed.

**You can view the revision history of a Deployment**:

```bash
kubectl rollout history deployment/my-app-deployment
```
