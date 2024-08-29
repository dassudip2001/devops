# **5.2 Secrets**

## 1. **Creating Secrets**

### **What are Secrets?**

- **Definition**: Secrets are Kubernetes objects used to store and manage sensitive information such as passwords, tokens, or keys. Unlike ConfigMaps, the data in Secrets is base64-encoded to offer a basic level of protection.

### **Creating Secrets**

#### 1. **From Literals**:

- You can create a Secret directly from key-value pairs using the `kubectl create secret` command.

```bash
kubectl create secret generic my-secret --from-literal=username=admin --from-literal=password=s3cr3t
```

- This creates a Secret named `my-secret` with two entries: `username=admin` and `password=s3cr3t`.

#### 2. **From Files**:

- You can create a Secret from a file. The file contents are encoded and stored as a value in the Secret.

```bash
kubectl create secret generic my-secret --from-file=path/to/secret/file
```

- If you have multiple files:

```bash
kubectl create secret generic my-secret --from-file=username=path/to/username --from-file=password=path/to/password
```

#### 3. **From Environment Files**:

- You can create a Secret from an environment file where each line of the file contains a key-value pair.

```bash
kubectl create secret generic my-secret --from-env-file=path/to/env/file
```

## 2. **Injecting Secrets into Pods Securely**

### **Mounting Secrets as Volumes**:

- You can mount a Secret as a volume inside a Pod. This allows your application to access sensitive information stored in files.

Example YAML for mounting a Secret as a volume:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secret-pod
spec:
  containers:
    - name: my-container
      image: nginx
      volumeMounts:
        - name: secret-volume
          mountPath: /etc/secret
  volumes:
    - name: secret-volume
      secret:
        secretName: my-secret
```

- In this example, the Secret `my-secret` is mounted at `/etc/secret` inside the container.

### **Using Secrets as Environment Variables**:

- You can inject Secret values as environment variables in your container.

Example YAML for using a Secret as environment variables:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: env-secret-pod
spec:
  containers:
    - name: my-container
      image: nginx
      env:
        - name: USERNAME
          valueFrom:
            secretKeyRef:
              name: my-secret
              key: username
        - name: PASSWORD
          valueFrom:
            secretKeyRef:
              name: my-secret
              key: password
```

- This injects the `username` and `password` from the `my-secret` Secret as environment variables in the container.

## 3. **Security Considerations**

### **Encrypting Secrets at Rest**:

- By default, Kubernetes stores Secrets as plaintext in `etcd`, but you can enable encryption at rest for Secrets.
- To enable encryption, you need to configure the Kubernetes API server with an encryption provider, such as `aescbc`.

### **RBAC Policies**:

- Control access to Secrets using Role-Based Access Control (RBAC). Define roles and role bindings to restrict which users or service accounts can access Secrets.

### **Controlling Access to Secrets**:

- Use service accounts with minimal permissions and restrict access to only the Secrets required by a specific application.

## 4. **Secret Types**

### **Opaque**:

- The default Secret type used for arbitrary user-defined data.

```bash
kubectl create secret generic my-secret --from-literal=username=admin --from-literal=password=s3cr3t
```

### **Docker Registry**:

- Used for storing Docker registry credentials.

```bash
kubectl create secret docker-registry my-docker-secret --docker-username=my-user --docker-password=my-pass --docker-email=my-email@example.com
```

### **TLS**:

- Used for storing TLS certificates and private keys.

```bash
kubectl create secret tls my-tls-secret --cert=path/to/tls.crt --key=path/to/tls.key
```

### **Basic Authentication**:

- Used for storing basic authentication credentials.

```bash
kubectl create secret generic my-basic-auth --from-literal=username=admin --from-literal=password=s3cr3t --type=kubernetes.io/basic-auth
```

## 5. **Updating and Rolling Secrets**

### **Updating Secrets**:

- Secrets can be updated using the `kubectl edit` command, but running Pods will not pick up the updated Secret automatically.

```bash
kubectl edit secret my-secret
```

### **Rolling Secrets**:

- To apply updated Secrets, you usually need to restart the Pods that consume them. This can be done by deleting the Pod or triggering a rollout for a Deployment.
- Example for a Deployment rollout:

```bash
kubectl rollout restart deployment/my-deployment
```

## 6. **Best Practices**

### **Avoid Hard-Coded Sensitive Data**:

- Never hard-code sensitive information in application code or Kubernetes manifests. Use Secrets instead.

### **Use External Secret Management Tools**:

- Consider using external secret management solutions like HashiCorp Vault, AWS Secrets Manager, or Azure Key Vault to manage and inject secrets into Kubernetes.

### **Regular Auditing**:

- Regularly audit your Secrets and access controls to ensure that they are secure and compliant with organizational policies.

### **Version Control**:

- Avoid committing base64-encoded secrets to version control. Instead, store unencoded files or use encrypted storage.

---
