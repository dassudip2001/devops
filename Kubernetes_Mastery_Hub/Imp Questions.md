# Imp Questins

---

## Kubernetes Garbage Collection

### What is Garbage Collection in Kubernetes?

- Its like an automatic cleanup crew.
- When you create, update, or delete things like pods or containers, garbage collection ensures that any leftovers or unused items are automatically identified and removed.

### Why Do We Need It?

- We need it to keep Kubernetes environment clean and efficient by preventing unnecessary stuf and freeing up resources.

### How Does it Work?

When you delete something (let's say a pod), it doesn't vanish instantly. It goes into a "Terminating" phase. Garbage collection then kicks in, cleans up the leftover bits (containers), and ensures everything is properly removed.

### What About Orphaned Pods?

If the thing that created a pod (resources) is gone (like a parent), and the pod is left alone (orphaned), garbage collection takes care of it. It's like making sure no one is left behind.

### The Process in Simple Steps:

- You say, "I don't need this pod anymore" (mark it for deletion).
- The pod goes into a "Terminating" phase (like packing up stuff).
- The containers within the Pod are killed.
- The **kubelet** performs garbage collection, deleting the dead containers.
- It does another round, cleaning up the terminated pods.
- If an image is lonely and not used by any pod, it gets removed during the next cleanup.

### Customizing Cleanup:

- You can tell Kubernetes how often to clean up and what to focus on.
- It's like setting a schedule for someone to come and clean your room regularly.

---

### How external services connect to the cluster?

External services connect to a cluster through methods like load balancers, service discovery, Ingress controllers (in Kubernetes), NodePort, assigning external IPs, VPNs, direct connections, and API gateways. The choice depends on factors like security and scalability.

---

### What is a headless service.?

service that dose not have **type** mentioned in its service.yml

---

A fun late-night production downtime story, around 1 year back when I was working on a new Kubernetes project hosted in EKS Cluster!

The project just hit production, and liveness and readiness probes were there but with fewer sec limits!

1 month went fine, then marketing campaigns began, and users started flooding, and accordingly load started increasing in the clusters, and mostly these promotions were in US timezones!

One such day I received a late-night call saying nothing working on, please fix (SOS)

Opened laptop, started checking things, and I saw cluster scaling but the pods were in an unhealthy state! and check desc, it was clear probes were failing! so increase the probes and after some trial and error stabilize it!

𝐍𝐨𝐭 𝐬𝐮𝐫𝐞 𝐰𝐡𝐚𝐭 𝐚𝐫𝐞 𝐭𝐡𝐞𝐬𝐞 𝐩𝐫𝐨𝐛𝐞𝐬?
A: In Kubernetes, probes are used to diagnose and take actions based on the state of containers within a pod

𝐓𝐡𝐞𝐫𝐞 𝐚𝐫𝐞 𝐭𝐡𝐫𝐞𝐞 𝐤𝐢𝐧𝐝𝐬 𝐨𝐟 𝐩𝐫𝐨𝐛𝐞𝐬:
𝐋𝐢𝐯𝐞𝐧𝐞𝐬𝐬 𝐏𝐫𝐨𝐛𝐞𝐬: Determine if a container is running. If a liveness probe fails, the kubelet kills the container, which will then be subjected to its restart policy.

𝐑𝐞𝐚𝐝𝐢𝐧𝐞𝐬𝐬 𝐏𝐫𝐨𝐛𝐞𝐬: Determine if a container is ready to serve requests. If a readiness probe fails, the endpoints controller removes the pod's IP address from the endpoints of all services that match the pod, effectively removing the pod from the service until it passes the readiness probe.

𝐒𝐭𝐚𝐫𝐭𝐮𝐩 𝐏𝐫𝐨𝐛𝐞𝐬: Determine if a container application has started. If a startup probe is configured, it disables liveness and readiness checks until it succeeds, ensuring that the application has enough time to start up before Kubernetes starts performing liveness or readiness checks.

Each of these probes can be configured to perform checks in one of the following ways:

HTTP GET: Performs an HTTP GET request to the container. The container is considered healthy if the response code is between 200 and 399.

TCP Socket: Tries to establish a TCP connection to the specified port of the container. The container is considered healthy if the connection is successful.

Exec: Executes a specified command inside the container. The container is considered healthy if the command exits with a status code of 0.

These probes can be configured with various parameters, such as initial delay (how long to wait before performing the first check), period (how often to perform the check), timeout (how long to wait for a check to pass before considering it failed), success threshold (how many times a probe must report success to be considered successful), and failure threshold (how many times a probe can fail before taking action).

Once again:
Careful configuration of these probes is crucial for maintaining the health and availability of applications running in Kubernetes.
