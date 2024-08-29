# ResourceQuota

## << --- In Progress --- >>

ResourceQuota in Kubernetes is like setting a budget for each team or project using the cluster. Just like you might have a budget for spending money, ResourceQuota helps you set limits on how much CPU, memory, storage, and other resources each part of your Kubernetes system can use.

For example, if you have multiple teams using the same Kubernetes cluster, you can make sure one team doesn't use up all the resources, leaving none for others. It's a way to keep things fair and ensure that the cluster runs smoothly without any one part hogging all the resources. Think of it as setting boundaries to prevent anyone from taking more than their fair share.

##### Here's everything you need to know about ResourceQuota:

1.  **Namespace Scope**: ResourceQuota applies at the namespace level. Each namespace can have its own ResourceQuota defined.
2.  **Resource Types**: ResourceQuota allows you to set limits on various types of resources such as CPU, memory, storage, and count of objects like Pods, Services, ConfigMaps, PersistentVolumeClaims, etc.
3.  **Specifying Limits**: You can specify usage limits for each resource type in terms of absolute values or as a percentage of the total cluster capacity.
4.  **ResourceQuota Object**: ResourceQuota is defined using a Kubernetes object of type `ResourceQuota`. This object contains the following fields:

    - `spec`: Specifies the resource limits.
    - `status`: Reports the current resource usage by the namespace against the defined limits.

5.  **Hard vs. Soft Limits**: ResourceQuota supports both hard and soft limits:

    - **Hard Limits**: When a hard limit is reached, Kubernetes rejects any new resource requests that would exceed the limit.
    - **Soft Limits**: Soft limits are advisory. Kubernetes does not enforce soft limits directly but can be used to monitor resource usage and trigger alerts or actions when exceeded.

6.  **Example Scenario**: Let's say you have a namespace dedicated to a particular team. You can define a ResourceQuota for that namespace specifying limits such as:

    - Maximum amount of CPU and memory that can be used by all Pods in the namespace.
    - Maximum number of Pods that can be created.
    - Maximum number of PersistentVolumeClaims (PVCs) that can be created.
    - Maximum amount of storage that can be claimed by PVCs.
    - And more depending on your specific requirements.

7.  **Monitoring**: Kubernetes provides mechanisms to monitor resource usage and limits through tools like Prometheus or by querying the Kubernetes API.
8.  **Management**: ResourceQuota can be managed using `kubectl` commands or through Kubernetes YAML configuration files.
9.  **Best Practices**:

    - Define ResourceQuotas for namespaces to prevent resource hogging and ensure fair resource distribution.
    - Regularly monitor resource usage and adjust ResourceQuota limits accordingly.
    - Consider using defaults ResourceQuotas for namespaces to avoid accidental resource exhaustion.

10. **Considerations**: While ResourceQuota helps in resource management, it's essential to carefully plan and set appropriate limits to avoid affecting application performance or causing disruptions.

### Example

Let's say you have a Kubernetes cluster where you want to limit the resources used by different namespaces. You have two teams, TeamA and TeamB, each working on separate projects. You want to make sure that neither team uses up all the resources and that they stay within their allocated limits.

Here's how you can set up ResourceQuota for each team:

1.  **Create Namespaces**: First, create namespaces for each team:

    ```yaml
    apiVersion: v1
    kind: Namespace
    metadata:
    name: team-a
    ---
    apiVersion: v1
    kind: Namespace
    metadata:
    name: team-b
    ```

2.  **Define ResourceQuota**: Next, define ResourceQuota objects for each namespace specifying the limits:

    ```yaml
    apiVersion: v1
    kind: ResourceQuota
    metadata:
    name: team-a-quota
    namespace: team-a
    spec:
    hard:
      pods: "10"
      requests.cpu: "4"
      requests.memory: 4Gi
      limits.cpu: "6"
      limits.memory: 6Gi
    ---
    apiVersion: v1
    kind: ResourceQuota
    metadata:
    name: team-b-quota
    namespace: team-b
    spec:
    hard:
      pods: "5"
      requests.cpu: "2"
      requests.memory: 2Gi
      limits.cpu: "3"
      limits.memory: 3Gi
    ```

    In this example:

    - `pods`: Maximum number of Pods that can be created.
    - `requests.cpu` and `requests.memory`: Maximum total amount of CPU and memory that can be requested by Pods.
    - `limits.cpu` and `limits.memory`: Maximum total amount of CPU and memory that can be limited by Pods.

3.  **Apply Configuration**: Apply these configurations to your Kubernetes cluster using `kubectl apply -f <filename>.yaml`.

With these ResourceQuota configurations, TeamA is allowed to create up to 10 Pods, with a total request limit of 4 CPU cores and 4Gi of memory, and a total limit of 6 CPU cores and 6Gi of memory. Similarly, TeamB is allowed to create up to 5 Pods, with a total request limit of 2 CPU cores and 2Gi of memory, and a total limit of 3 CPU cores and 3Gi of memory.
