# StatefulSets

## What is StatefulSets.?

- It manages the deployment and scaling of a set of pods, but with a **focus on** maintaining a stable and unique identity for each pod.
- It dose same work as Deployments (its NOT for stateless applications), BUT for stateful applications.
- It just like Deployments + it maintains unique identity of Pods.

### Stateless vs Stateful

#### **Stateful Application**:

- An app that remembers things between uses. That second request will know what the first request is about.

- An application that maintains data or state between client interactions or requests, **requiring persistent storage** and often retaining information about past interactions.

#### **Stateless Application**:

- An app that forgets things after each use.

- An application that does not retain client data or state between interactions, treating each request as independent and not relying on stored data from previous requests.

### Deployments vs StatefulSets

|                   | **Deployments**                                                                                                 | **StatefulSets**                                                                                                |
| ----------------- | --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| **Category**      | Best for stateless applications                                                                                 | Ideal for stateful applications                                                                                 |
| **Best for**      | Stateless applications                                                                                          | Applications that require persistent storage and stable network identities                                      |
| **Suited for**    | Scalable, ephemeral workloads                                                                                   | Suited for databases, messaging systems, and applications with dependencies on ordered scaling or startup order |
| **Efficient for** | Web servers, microservices, and applications without strict data persistence or ordered deployment requirements | Databases, messaging systems, and applications with dependencies on ordered scaling or startup order            |
| **Use Cases**     | E-commerce platforms, Blogs, Content Delivery Networks                                                          | MySQL databases, Apache Kafka, Legacy applications with stateful requirements                                   |

---

### Use Cases for StatefulSets in Stateful Applications

1.  **Databases (e.g., MySQL, PostgreSQL):**

    - Ideal for databases, ensuring data consistency and ordered scaling. Each instance has a stable network identity for seamless communication.

2.  **Messaging Systems (e.g., Apache Kafka):**

    - Beneficial for message queues like Apache Kafka.
    - Stable network identity and persistent storage ensure reliable messaging even during pod rescheduling.

3.  **Distributed File Systems (e.g., Ceph, GlusterFS):**

    - Well-suited for distributed file systems, providing stable identities and persistent storage for shared data.

4.  **Legacy Applications with Stateful Requirements:**

    - Facilitates transitioning or maintaining compatibility with legacy applications relying on stateful deployment models.

#### Benefits:

1.  **Stable Network Identities:**

    - Each pod gets a unique, stable hostname, crucial for consistent communication between instances.

2.  **Persistent Storage:**

    - Utilizes Persistent Volumes (PVs) and Persistent Volume Claims (PVCs) for data persistence across rescheduling or replacements.

3.  **Ordered Scaling:**

    - Maintains order during deployment and scaling, beneficial for applications with startup dependencies.

4.  **Headless Service for DNS-Based Discovery:**

    - Automatically creates a headless service, enabling DNS-based service discovery for easy communication between pods.

---
