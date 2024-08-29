# P.1 Scaling with ReplicaSets

#### Description:

- Deploy an application with ReplicaSets and observe how Kubernetes maintains the specified number of replicas.

### Step 1: Set up your Kubernetes Cluster

Before we dive into ReplicaSets, make sure you have a Kubernetes cluster up and running.

### Step 2: Create the Deployment YAML

Firstly, we'll define the deployment for our application. A Deployment manages a ReplicaSet and ensures that the specified number of replicas are running at all times.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: todo-container
          image: nginx:latest
          ports:
            - containerPort: 80
```

### Step 3: Apply the Deployment

Save the YAML file, and apply it to your Kubernetes cluster using the following command:

```bash
kubectl apply -f <your-deployment-file-name.yaml>
```

<img src="../Img/4.P.1-Apply-Deployment.png">

### Step 4: Check the Deployment

Verify that the Deployment has been created successfully:

```bash
kubectl get deployments
```

### Step 5: Observe ReplicaSets

Now, let's see how ReplicaSets come into play. Behind the scenes, Kubernetes will create a ReplicaSet for our Deployment.

```bash
kubectl get replicasets
```

### Step 6: Scale the Deployment

Let's test scaling. Change the number of replicas in your Deployment YAML file and apply the changes:

```bash
spec:
  replicas: 5
```

```bash
kubectl apply -f <your-deployment-file-name.yaml>
```

<img src="../Img/4.P.1-Scale-Deployment.png">

Observe how Kubernetes adjusts the number of pods to meet the desired state.

### Step 7: Monitor the Pods

Check the running pods:

```bash
kubectl get pods
```

### Step 8: Clean Up

```bash
kubectl delete deployment <your-deployment-name>
```

<img src="../Img/4.P.1-delete-Deployment.png">

Finally, when you're done, clean up the resources.

---
