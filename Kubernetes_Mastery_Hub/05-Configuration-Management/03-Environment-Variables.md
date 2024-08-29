# **5.3 Environment Variables**

## 1. **Basics of Environment Variables**

### **What are Environment Variables?**

- **Definition**: Environment variables are key-value pairs that are passed into containers at runtime. They can be used by applications to configure settings, paths, or any other dynamic data.

### **Why Use Environment Variables?**

- They allow you to change the configuration of your application without altering the code.
- They help in separating configuration from the code, making applications more portable and easier to manage.

## 2. **Passing Environment Variables**

### **Defining Environment Variables in Pod Specs:**

- You can define environment variables directly in the Pod spec using the `env` field in the container definition.

Example YAML:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: env-var-pod
spec:
  containers:
    - name: my-container
      image: nginx
      env:
        - name: MY_ENV_VAR
          value: "my-value"
```

- In this example, `MY_ENV_VAR` is set to `my-value` inside the container.

### **Setting Multiple Environment Variables:**

- You can define multiple environment variables in the same way:

```yaml
env:
  - name: MY_ENV_VAR1
    value: "value1"
  - name: MY_ENV_VAR2
    value: "value2"
```

## 3. **Using Environment Variables from ConfigMaps and Secrets**

### **Injecting Environment Variables from ConfigMaps:**

- You can inject values from a ConfigMap into your container as environment variables.

Example YAML:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: configmap-env-pod
spec:
  containers:
    - name: my-container
      image: nginx
      envFrom:
        - configMapRef:
            name: my-config
```

- This injects all key-value pairs from the `my-config` ConfigMap as environment variables.

### **Injecting Specific Environment Variables from ConfigMaps:**

- You can inject specific entries from a ConfigMap into the container's environment.

Example YAML:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: specific-configmap-env-pod
spec:
  containers:
    - name: my-container
      image: nginx
      env:
        - name: MY_ENV_VAR
          valueFrom:
            configMapKeyRef:
              name: my-config
              key: my-key
```

- This injects the value associated with `my-key` in `my-config` ConfigMap into `MY_ENV_VAR`.

### **Injecting Environment Variables from Secrets:**

- Secrets can also be used to inject sensitive data as environment variables.

Example YAML:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secret-env-pod
spec:
  containers:
    - name: my-container
      image: nginx
      env:
        - name: MY_SECRET_VAR
          valueFrom:
            secretKeyRef:
              name: my-secret
              key: my-secret-key
```

- This injects the value associated with `my-secret-key` in `my-secret` Secret into `MY_SECRET_VAR`.

## 4. **Environment Variable Substitution**

### **Using Existing Environment Variables to Define New Ones:**

- Kubernetes allows you to define new environment variables based on existing ones, using the `valueFrom` and `fieldRef` fields.

Example YAML:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: env-substitution-pod
spec:
  containers:
    - name: my-container
      image: nginx
      env:
        - name: MY_VAR
          value: "Hello"
        - name: MY_NEW_VAR
          value: "$(MY_VAR), World!"
```

- In this example, `MY_NEW_VAR` will be set to "Hello, World!" based on the value of `MY_VAR`.

### **Referencing Pod Fields in Environment Variables:**

- You can reference specific fields of the Pod in environment variables, such as the Pod’s name, namespace, or IP.

Example YAML:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: fieldref-env-pod
spec:
  containers:
    - name: my-container
      image: nginx
      env:
        - name: POD_NAME
          valueFrom:
            fieldRef:
              fieldPath: metadata.name
        - name: POD_NAMESPACE
          valueFrom:
            fieldRef:
              fieldPath: metadata.namespace
```

- This sets `POD_NAME` to the Pod’s name and `POD_NAMESPACE` to the Pod’s namespace.

### **Combining Multiple Values:**

- You can also combine multiple values using environment variable substitution.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: combined-env-pod
spec:
  containers:
    - name: my-container
      image: nginx
      env:
        - name: COMBINED_VAR
          value: "$(POD_NAME)-$(POD_NAMESPACE)"
```

- This creates `COMBINED_VAR` by combining the Pod’s name and namespace.

---
