# About manifest file

| Core Kubernetes Resources (`apiVersion: v1`) | Higher-level Abstractions (`apiVersion: apps/v1`) |
| -------------------------------------------- | ------------------------------------------------- |
| Pod                                          | Deployment                                        |
| Service                                      | ReplicaSet                                        |
| Namespace                                    | StatefulSet                                       |
| ConfigMap                                    | DaemonSet                                         |
| Secret                                       | Job                                               |
|                                              | CronJob                                           |
|                                              | ServiceAccount                                    |

## One line Explanations

### Core Kubernetes Resources (`apiVersion: v1`)

1. **Pod:** The smallest deployable units in Kubernetes.
2. **Service:** Enables communication between different sets of Pods.
3. **Namespace:** Provides a way to divide cluster resources between multiple users or projects.
4. **ConfigMap:** Allows you to decouple configuration artifacts from image content to keep containerized applications portable.
5. **Secret:** Holds sensitive information, such as passwords, OAuth tokens, and SSH keys.

### Higher-level Abstractions (`apiVersion: apps/v1`)

1. **Deployment:** Manages the deployment and scaling of a set of Pods, providing declarative updates to applications.
2. **ReplicaSet:** Ensures a specified number of replicas of a Pod are running at all times.
3. **StatefulSet:** Manages the deployment and scaling of a set of Pods with unique identities, stable network identities, and persistent storage.
4. **DaemonSet:** Ensures that all (or some) Nodes run a copy of a Pod, typically used for system daemons.
5. **Job and CronJob:** Creates one or more Pods and ensures that a specified number of them successfully terminate.
6. **ServiceAccount:** Provides an identity for processes that run in a Pod.

---

Q) what is difference between different `apiVersion`?
