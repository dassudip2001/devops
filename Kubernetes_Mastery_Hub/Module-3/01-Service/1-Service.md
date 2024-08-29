# Services

## What is a Service?

Its a component that provide's a stable endpoint (IP address and port) for a set of pods, enabling seamless communication and discovery within the cluster.

- **Used for:** Communication within the cluster and exposing the port to the enduser.

## Why do we need Service?

- **Pods are constantly replaced:** In Kubernetes, Pods are frequently killed and replaced to maintain the desired state of the cluster.

- **Challenge of dynamic communication:** This constant change makes it difficult for applications within the cluster to reliably communicate with each other.

- **Introduction of Kubernetes Services:** Kubernetes Services address this challenge by providing a consistent and stable way for applications to access each other.

- **Stable communication endpoints:** Services offer fixed endpoints that remain the same even as Pods come and go, ensuring seamless communication between applications.

- **Simplified cluster management:** By abstracting away the complexities of dynamic Pod management, Services make it easier to manage and maintain applications within Kubernetes clusters.

## Main goals of Services are:

- **Load balancing:** Traffic is distributed among pods to prevent overload.
- **Discovery and routing:** As Pods scale up or down, Services makes sure they get IP address and port.
- **Stable network endpoint:**
- **Decoupling:** <u>It keeps stable connections</u>. Separates your logical app view from physical pod changes, simplifying management.

## How Services work:

- **Labels and Selectors**: Services use labels to select Pods to include in their set. Labels on Pods are matched to selectors defined in the Service configuration.

- **Endpoints**: Each Service maintains a set of endpoints (IP addresses and ports) corresponding to the Pods it selects. Kubernetes automatically updates these endpoints as Pods are created, deleted, or modified.

- **Service Discovery**: Services provide a way for other parts of your application to discover and communicate with Pods without needing to know their individual IP addresses.

- **Load Balancing**: Depending on the type of Service, Kubernetes may provide load balancing capabilities. For example, a ClusterIP Service will load balance traffic across all selected Pods.

### Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    app.kubernetes.io/name: proxy
spec:
  containers:
    - name: nginx
      image: nginx:stable
      ports:
        - containerPort: 80
          name: http-web-svc

---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app.kubernetes.io/name: proxy
  ports:
    - name: name-of-service-port
      protocol: TCP
      port: 80
      targetPort: http-web-svc
```

- **targetPort**: is the port on the Pod to which traffic should be forwarded.

#### let's break down how the Services work in this example:

1.  **Pod Definition**:

    - The YAML defines a Pod named "nginx" with the **label** "app.kubernetes.io/name: proxy".
    - It runs an Nginx container listening on port 80.

2.  **Service Definition**:

    - The YAML defines a Service named "nginx-service".
    - It selects by matching the **selector** of service with Pods **label** "app.kubernetes.io/name: proxy".
    - It **exposes** port 80 as the service port.
    - It maps incoming traffic on port 80 to the **targetPort "http-web-svc"**, which is the **containerPort** 80 of the Pod.

3.  **Labels and Selectors**:

    - The Service selects Pods with the label "app.kubernetes.io/name: proxy", which matches the label set in the Pod definition.
    - This ensures that the Service will route traffic to the Pod we want (in this case, the Nginx Pod).

4.  **Endpoints**:

    - The Service maintains a list of endpoints, which includes the IP address and port of the Pod(s) it selects.
    - In this case, the Service will keep track of the IP address and port of the Nginx Pod.

5.  **Service Discovery**:

    - Other parts of your application can now communicate with the Nginx Pod using the Service name "nginx-service" and the port specified in the Service definition (port 80).
    - They don't need to know the specific IP address or port of the Pod; they can simply use the Service name to access it.

6.  **Load Balancing**:

    - If you have multiple Pods with the same label and they are all selected by the Service, Kubernetes will automatically load balance incoming traffic across these Pods.
    - In this example, if you scale up the number of Nginx Pods, the Service will distribute incoming requests among them.

---

#### Key Components of a Service:

- **Service IP:**

  - **ClusterIP**: Internal IP for communication within the cluster.
  - **NodePort**: Exposes the service on each node's IP at a static port.
  - **LoadBalancer**: Automatically assigns an external IP.

- **Port Mapping:**

  - Define the port on which the service can be accessed.

---
