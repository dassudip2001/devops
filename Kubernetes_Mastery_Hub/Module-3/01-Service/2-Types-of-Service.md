# Types of Kubernetes Services

### 1. ClusterIP Service

- Used for **Internal Communication** within the cluster. It is the **default** service.
- It assigns an internal IP that is only reachable from within the cluster.
- **Why:** If your application components (pods) need to talk to each other within the cluster **ONLY**.
- It exposes the service on an internal IP within the cluster, thus, Suitable for microservices.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: MyApp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 9376
```

### 2. NodePort Service

- Used for **External Access to Nodes** outside the cluster, not from Internet.

- Exposes the service on each node's IP at a static port.

- **Why:** When you want to access your service from outside the cluster, but you don't want to manage **LoadBalancers**.

- Manageable for small-scale setups but may pose challenges in larger deployments.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: MyApp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 9376
  type: NodePort
```

### 3. LoadBalancer:

- Used for **Automated External Access** to the internet.

- It triggers external IP assignment.

- **Why:** When K8s LoadBalancer services is used, it triggers(or provisions) the activation of a cloud-based LoadBalancer provided by your cloud provider. The cloud-based LoadBalancer gets an external IP, and that IP becomes the entry point for external traffic to reach your application within the Kubernetes cluster.

- Suitable for production environments requiring reliability and scalability.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: MyApp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 9376
  type: LoadBalancer
```

### 4. ExternalName:

> Its very less used, so many people ignore it.

- Used for mapping a Service to an external DNS name.
- **Why:** When **you** want to provide access to an external service by DNS name instead of IP address.
- It does not have selectors or endpoints; instead, it simply returns a CNAME record with the specified external name.
- Suitable for integrating Kubernetes services with external services without exposing internal details.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
  namespace: prod
spec:
  type: ExternalName
  externalName: my.database.example.com
```

- This allows applications within the cluster to access "my.database.example.com" without needing to know its IP address.

---

##### Diagram representing communication paths between different components in a Kubernetes cluster:

```scss
+-----------------------------------------------------------------------------------+
|                                     INTERNET                                      |
+-----------------------------------------------------------------------------------+
                  |
                  |
                  v
+-----------------------------+   NodePort/LoadBalancer   +-----------------+
|         LoadBalancer        |  <----------------------> |   Node(s)       |
|        (External IP)        |                           |                 |
+-----------------------------+                           +-----------------+
                  |
                  |
                  v
+-----------------------------------------------------------------------------------+
|   +-----------------------------+   ClusterIP    +-----------------------------+  |
|   |         Node(s)             | <------------> |         Node(s)             |  |
|   |    (Internal Cluster IP)    |                |    (Internal Cluster IP)    |  |
|   +-----------------------------+                +-----------------------------+  |
|          Kubernetes Cluster (Nodes, Pods, Services, etc.)                         |
+-----------------------------------------------------------------------------------+
```

> Keep in mind that this is a textual representation, and the actual architecture may vary based on your specific Kubernetes setup and networking configuration.

---
