# Simple Nginx Pod

**Description**: Deploy a simple web server using a Pod manifest. Experiment with different configurations such as environment variables and commands.

Step 0:- Install and configure the K8s cluster.

Step 1:- Create the Manifest file
: - Write the "desired state", and save the YAML manifest file, on **control-plane**. let's say `example-pod.yaml`.

```yml
apiVersion: v1
kind: Pod
metadata:
  name: example-pod
  labels:
    app: example
spec:
  containers:
    - name: container-1
      image: nginx:latest
      ports:
        - containerPort: 80
  restartPolicy: Always
```

Step 2:- Apply the Manifest
: - Navigate to the dir where the YAML file is saved and run the following command:

For first time.

```bash
kubectl create -f <name_of_the_file>.yaml
```

Updating the pod.

```bash
kubectl apply -f example-pod.yaml
```

Step 3:- Check Pod Status.
: - Wait until the Pod's STATUS becomes **"Running"**.

```bash
kubectl get pods
```

---

#### Verify by browser

> **Note:-** This example is without the **Service** so you have to Expose the Nginx Pod port manually.

Step 4:- Expose the Nginx Pod
: - It creates a **service** of type **`NodePort`** that maps port `80` of the pod to a port on your nodes.
: - Will get --> `service/example-pod exposed`

```bash
kubectl expose pod example-pod --type=NodePort --port=80
```

- relpace `example-pod` with your **pod name**.

Step 5:- Get the NodePort
: - Now find out the NodePort assigned to the service.
: - The NodePort will be listed under the `PORT(S)` column, eg: **`80:30312/TCP`**.

```bash
kubectl get services
```

- **`80`**: **Container Port**, where your Nginx container inside the Pod is listening.
- **`30312`**: **NodePort**, external port <u>on each node</u> that redirects to the container port **`80`** inside the cluster.
- **`TCP`**: Protocol being used.

Step 6:- Access in Browser:
: - Replace `<node_ip>` with the **IP address** of any node in your Kubernetes cluster and `<NordPort>` with actual **NordPort**.

```bash
http://<node_ip>:<NordPort>
```

- For example, if the IP address of your node is `192.168.0.2` and NordPort is `30312`, then **`http://192.168.0.2:30312`**.
- It will show Nginx welcome page.

---

### Simple diagram to illustrate how the ports are working:

```bash
+------------------------+            +------------------------+
|                        |            |                        |
|       External         |            |        Kubernetes      |
|       Browser          |            |         Cluster        |
|                        |            |                        |
+-----------+------------+            +-----------+------------+
            |                                       |
            |                                       |
            v                                       v
+-----------+------------+            +-----------+------------+
|                        |            |                        |
|    Node's IP:30312     +----------->+   Service:example-pod  |
|                        |            |    Port Mapping:       |
+------------------------+            |    80:30312/TCP        |
                                      |                        |
                                      +-----------+------------+
                                                 |
                                                 |
                                                 v
                                        +--------+---------+
                                        |                  |
                                        |   Pod:example-   |
                                        |   pod            |
                                        |   Container      |
                                        |   Port: 80       |
                                        +------------------+
```

#### In this diagram:

- The External Browser communicates with a Node's IP on port `30312`.
- The **NodePort** (`30312`) redirects the traffic to the **Service**, which then forwards it to the Pod's Nginx **container** on port `80`.

---

## Adittional Commands

Delete Pod
: To delete pod use.,

```bash
kubectl delete pod <pod-name>
```

View Pod Details:
: To get more **details of the running pod** use.,

```bash
kubectl describe pod <pod-name>
```

This command provides comprehensive information about the pod, including events and conditions.

Accessing Pod Logs:
: To view the logs of a container within the pod, use kubectl logs.

```bash
kubectl logs mypod -c mycontainer
```

Replace mypod with your pod's name and mycontainer with your container's name.
