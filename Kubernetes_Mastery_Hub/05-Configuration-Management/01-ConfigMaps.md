# **5.1 ConfigMaps**

## 1. **Creating and Managing ConfigMaps**

### **What are ConfigMaps?**

- **Definition**: ConfigMaps are Kubernetes objects used to store non-confidential data in key-value pairs. These can be used to pass configuration data to your application without hard-coding it into your application image.

### **Creating ConfigMaps**

#### 1. **From Literals**:

- You can create a ConfigMap directly from key-value pairs using the `kubectl create configmap` command.

```bash
kubectl create configmap my-config --from-literal=key1=value1 --from-literal=key2=value2
```

This creates a ConfigMap named `my-config` with two entries: `key1=value1` and `key2=value2`.

#### 2. **From Files**:

- You can create a ConfigMap from a file or a set of files. Each file will be stored as a key in the ConfigMap, with its contents as the value.

```bash
kubectl create configmap my-config --from-file=path/to/config/file
```

- If you have multiple files:

```bash
kubectl create configmap my-config --from-file=config1=path/to/config1 --from-file=config2=path/to/config2
```

#### 3. **From Directories**:

- You can create a ConfigMap from a directory, where each file in the directory becomes a key in the ConfigMap.

```bash
kubectl create configmap my-config --from-file=path/to/directory/
```

## 2. **Injecting ConfigMaps into Pods**

### **Mounting ConfigMaps as Volumes**:

- You can mount a ConfigMap as a volume inside a Pod. This allows your application to access configuration files directly from the filesystem.

Example YAML for mounting a ConfigMap as a volume:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: configmap-pod
spec:
  containers:
    - name: my-container
      image: nginx
      volumeMounts:
        - name: config-volume
          mountPath: /etc/config
  volumes:
    - name: config-volume
      configMap:
        name: my-config
```

- In this example, the ConfigMap `my-config` is mounted at `/etc/config` inside the container.

### **Using ConfigMaps as Environment Variables**:

- You can inject ConfigMap values as environment variables in your container.

Example YAML for using a ConfigMap as environment variables:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: env-pod
spec:
  containers:
    - name: my-container
      image: nginx
      envFrom:
        - configMapRef:
            name: my-config
```

- This injects all key-value pairs from the `my-config` ConfigMap as environment variables.

## 3. **Updating ConfigMaps**

### **Handling Updates**:

- Updating a ConfigMap doesn’t automatically update running Pods that consume it. The Pods will continue to use the old version of the ConfigMap until they are restarted.
- Best Practice: Use rolling updates or recreate Pods to pick up the new configuration.

### **Updating a ConfigMap**:

```bash
kubectl edit configmap my-config
```

- This command opens the ConfigMap in your default text editor, where you can make changes. Once you save and exit, the ConfigMap is updated.

## 4. **Best Practices**

### **Naming Conventions**:

- Use descriptive names that reflect the purpose of the ConfigMap, like `app-config`, `database-config`, etc.

**Version Control**:

- Store your ConfigMaps in source control as YAML files. This allows you to track changes and roll back if needed.

### **Managing Large Configurations**:

- Break large configurations into multiple ConfigMaps to keep them manageable.

## 5. **ConfigMap as Command Line Arguments**

### **Passing Values as Command-Line Arguments**:

- You can use values from ConfigMaps as command-line arguments for your containers.

Example YAML:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: cmdline-pod
spec:
  containers:
    - name: my-container
      image: my-app
      args:
        - "--config"
        - "/etc/config/config-file"
      volumeMounts:
        - name: config-volume
          mountPath: /etc/config
  volumes:
    - name: config-volume
      configMap:
        name: my-config
```

- In this example, the command-line argument `--config` points to a configuration file provided by the ConfigMap.

---
