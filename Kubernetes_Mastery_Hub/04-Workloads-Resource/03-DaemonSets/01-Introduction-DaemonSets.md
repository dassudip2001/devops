# DaemonSets

**Official k8s Docs:** https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/

System Daemon
: In the context of Kubernetes, it refers to a **background process** or **service** that runs on each node in the cluster.

## What is DaemonSets.?

**It's JOB is to runs a copy of a pod on every node within a cluster.**

## How it is done.?

- You write the manifest file. Named **daemonset-demo.yaml**

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: example-daemonset
spec:
  selector:
    matchLabels:
      app: example
  template:
    metadata:
      labels:
        app: example
    spec:
      containers:
        - name: example-container
          image: example-image:latest
```

1. **Understanding the DaemonSet:**

   - This is a Kubernetes resource of type `DaemonSet`, named `example-daemonset`.
   - It specifies that it should target **nodes** with a label `app: example`.

     - labels are associated with **nodes** as well as **pods**. When we say the DaemonSet targets nodes with a specific label, it means that the DaemonSet looks for **nodes** that have been labeled with a certain key-value pair.

2. **Labeling Nodes:**

   - **Before applying the DaemonSet**, you need to label the **nodes** where you want the pods to run.
   - For example, label a node using:

     ```bash
     kubectl label nodes <node-name> app=example
     ```

   - This command adds a label `app: example` to the specified node.

3. **Apply**

   ```bash
   kubectl apply -f daemonset-demo.yaml
   ```

4. **DaemonSet Selection:**

   - The DaemonSet will automatically identify **nodes** with the label `app: example`.
   - It will create and manage one pod on each of these labeled nodes.

## Node Affinity and Anti-Affinity

- You can define node selectors, node affinity, or anti-affinity rules to control which nodes the DaemonSet pods are scheduled on.
- This gives you fine-grained control over pod placement based on node characteristics or other factors.

## Scaling

- DaemonSets automatically scale the number of instances based on the number of nodes in the cluster.
- If new nodes are added, DaemonSets ensure that pods are scheduled on these nodes as well.
- Similarly, if nodes are removed, DaemonSets terminate pods on those nodes.

## DaemonSets Use Cases:

1.  **Logging Agent**:

    - **Use Case**: Deploying a logging agent on every node to collect logs.
    - **Example**: Fluentd or Fluent Bit DaemonSet collecting application logs from every node and forwarding them to a centralized logging system like Elasticsearch.

2.  **Monitoring Agent**:

    - **Use Case**: Installing a monitoring agent on every node to collect metrics.
    - **Example**: Prometheus Node Exporter DaemonSet gathering system-level metrics such as CPU, memory, and disk usage from each node for monitoring purposes.

3.  **Networking Plugin**:

    - **Use Case**: Deploying a networking plugin to manage network connectivity.
    - **Example**: Calico or Weave DaemonSet ensuring network policies and connectivity are consistently managed across all nodes in the cluster.

4.  **Security Agent**:

    - **Use Case**: Installing security agents for vulnerability scanning or intrusion detection.
    - **Example**: Falco or Sysdig DaemonSet monitoring system calls and detecting abnormal behavior or security threats on every node.

5.  **Load Balancer Controller**:

    - **Use Case**: Deploying a load balancer controller to manage traffic distribution.
    - **Example**: Nginx or HAProxy DaemonSet providing load balancing functionality for services running on each node.

6.  **Storage Plugin**:

    - **Use Case**: Installing a storage plugin to manage distributed storage across the cluster.
    - **Example**: GlusterFS or Ceph DaemonSet ensuring that distributed storage volumes are available on every node for persistent storage needs.

7.  **DNS Resolver**:

    - **Use Case**: Deploying a DNS resolver to handle service discovery within the cluster.
    - **Example**: CoreDNS DaemonSet ensuring DNS resolution for Kubernetes services and pods on each node.

8.  **Custom Daemon or Agent**:

    - **Use Case**: Deploying a custom daemon or agent specific to your application or infrastructure needs.
    - **Example**: A custom DaemonSet collecting application-specific metrics or performing background tasks required by your application.
