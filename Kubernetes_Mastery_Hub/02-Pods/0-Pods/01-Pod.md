# Pods

**Official k8s Docs:** https://kubernetes.io/docs/concepts/workloads/pods/

#### files -> image -> container -> pod

---

#### 1. What is a Pod?

A Pod in Kubernetes is the smallest deployable unit, encapsulating one or more containers and shared resources like networking and storage volumes, serving as the basic building block for deploying and managing applications in the cluster.

##### Example of a Pods

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
    - name: nginx
      image: nginx:1.14.2
      ports:
        - containerPort: 80
```

#### 2. Types of Containers inside Pod

#### i) Main Application Container

This is the primary container that runs your application or service.

#### ii) Sidecar Container

- They run alongside the main application container within the same Pod.

- **Use cases for sidecar containers:**
  - Logging
  - Monitoring
  - Security
  - Proxying

#### iii) Init Containers

- Special containers that run before the main application containers, **performing setup tasks**.
- It's like a friend who arranges the game before everyone else joins.

#### iv) Ephemeral Containers

- Temporary containers for **debugging purposes**, injected into a running Pod when needed.
- Its like a friend who is not playing but can be called if anything goes worng, or like an umpire in cricket.

#### 3. Pods go through various phases, that are:

- **Pending**: The Pod is accepted by the system, and resources are being allocated.
- **Running**: All containers in the Pod are running, and at least one is in the running phase.
- **Succeeded**: All containers in the Pod have terminated successfully.
- **Failed**: All containers in the Pod have terminated, and at least one container has failed.
- **Unknown**: The state of the Pod cannot be determined.

#### 4. What considerations should be taken into account when scaling applications horizontally using multiple Pods?

- Each Pod should ideally run a single instance of the application.
- Allocate **appropriate compute resources** (CPU, memory) for each Pod.
- Implement **load balancing** to evenly distribute incoming traffic.
- Set up **health checks** and **monitoring** for each Pod.
- Consider enabling **auto-scaling** based on metrics like **CPU utilization**.
- Design applications to be **stateless** for easier scaling.
- Configure persistent storage solutions if needed for data storage.

#### 5. How does Kubernetes handle updates to Pod templates, and what impact does this have on existing Pods?

1.  Kubernetes first creates new Pods based on the updated template.
2.  The kubelet initializes the new Pods by pulling container images.
3.  New Pods are scheduled on suitable nodes.
4.  Finally, Kubernetes terminates the old Pods.
5.  This process ensures the app is never stopped.

#### 6. Can you explain the networking model for Pods in Kubernetes, including how communication is managed within and outside of Pods?

- Each Pod is assigned a unique IP address, and containers within the Pod share the network namespace.
- Communication **within** the Pod occurs via localhost, while communication **outside** the Pod requires coordination of shared network resources.

#### 7. What are Static Pods, and in what scenarios would you use them instead of dynamically managed Pods?

Static Pods in Kubernetes are essentially identical copies of control plane components (kube-apiserver, kube-controller-manager, and kube-scheduler), managed directly by the kubelet on a specific node.

It is useful in scenarios where you need fine-grained control over critical system components without relying on the Kubernetes control plane.

#### 8. How do container probes function in Kubernetes, and why are they important for ensuring the health and availability of applications running in Pods?

- Container probes are **diagnostic checks** performed periodically by the kubelet on a container to ensure its health and availability.
- Probes can be of different types, such as **ExecAction**, **TCPSocketAction**, or **HTTPGetAction**, and they help Kubernetes manage the lifecycle of Pods effectively.

---

### Benefits:

- **Efficient Communication**: Containers share resources like volumes, IPC, and network namespace.
- **Data Locality**: Access shared resources locally, reducing latency.
- **Tightly Coupled Management**: Orchestrated as a single unit for simplified operations.

### Communication:

- **Shared Volumes**: Persistent storage for data exchange.
- **IPC Namespace**: Containers share IPC namespace, facilitating communication.
- **Network Namespace**: Containers use same network namespace, simplifying communication over localhost.

### Use Cases:

- **Sidecar Containers**: Using other container as, log watchers or monitoring, without bothering the main container.
- **Proxies/Adapters**: Using other container as, proxies, bridges, or adapters connecting the main container with external services or networks, thus improving communication and integration capabilities.
- **Modular Applications**: Modular Applications means, an application which is built with multiple small block or containers, so each team can work on their own container, it encourage code reuse and collaboration among teams.

---
