# P.2 Rolling Updates and Rollbacks

#### Description:

- Deploy a sample app, make changes to the deployment manifest, and observe rolling updates. Practice rollbacks in case of issues.

### Step 1: Deploy the Initial Application

Start by creating a simple Deployment YAML for your sample app. Save it in a file, let's say `your-app-deployment.yaml`.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: your-app-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: your-app
  template:
    metadata:
      labels:
        app: your-app
    spec:
      containers:
        - name: your-app-container
          image: your-docker-image:version1
          ports:
            - containerPort: 80
```

Apply the deployment to your cluster:

```bash
kubectl apply -f your-app-deployment.yaml
```

### Step 2: Observe the Deployment

Ensure that your pods are running:

```bash
kubectl get pods
```

### Step 3: Make Changes for Rolling Update

Now, let's make a change in your deployment manifest. Update the image version to trigger a rolling update. Save the changes in `your-app-deployment.yaml`.

```yaml
spec:
  template:
    spec:
      containers:
        - name: your-app-container
          image: your-docker-image:version2
```

Apply the changes:

```bash
kubectl apply -f your-app-deployment.yaml
```

### Step 4: Observe Rolling Update

Check the status of the rolling update:

```bash
kubectl rollout status deployment your-app-deployment
```

Observe how Kubernetes gradually replaces old pods with new ones to ensure a smooth update.

### Step 5: Rollback in Case of Issues

If any issues arise during the rolling update, you can perform a rollback:

```bash
kubectl rollout undo deployment your-app-deployment
```

This will revert to the previous version, and you can monitor the rollback status:

```bash
kubectl rollout status deployment your-app-deployment
```

### Step 6: Verify Rollback

Check the pods to ensure they are running the previous version:

```bash
kubectl get pods
```

You've successfully executed a rolling update and rollback in Kubernetes.

---
