# Creating manifest files

Creating Kubernetes manifest files using the `kubectl create` command is a fundamental skill for managing Kubernetes resources. The `kubectl create` command can generate manifest files for various Kubernetes resources such as Pods, Deployments, Services, ConfigMaps, and more. Below, we will explore the usage of the `kubectl create` command, along with detailed examples for different types of resources.

### 1. Overview of `kubectl create` Command

The `kubectl create` command is used to create resources in a Kubernetes cluster. It can also generate YAML or JSON manifest files that define these resources. The basic syntax of the `kubectl create` command is:

```sh
kubectl create <resource> [options]
```

### 2. Generating Manifest Files

You can generate manifest files using the `--dry-run=client -o yaml` options. This allows you to see the YAML configuration without actually creating the resource in the cluster.

### 3. Common Resource Types and Examples

#### Creating a Pod

A Pod is the smallest deployable unit in Kubernetes. It represents a single instance of a running process in your cluster.

**Command:**

```sh
kubectl create pod my-pod --image=myimage --dry-run=client -o yaml
```

**Output:**

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: my-pod
      image: myimage
```

#### Creating a Deployment

A Deployment provides declarative updates to applications. It manages the deployment of ReplicaSets and ensures the desired state is maintained.

**Command:**

```sh
kubectl create deployment my-deployment --image=myimage --dry-run=client -o yaml
```

**Output:**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-deployment
  template:
    metadata:
      labels:
        app: my-deployment
    spec:
      containers:
        - name: my-deployment
          image: myimage
```

#### Creating a Service

A Service is an abstract way to expose an application running on a set of Pods as a network service.

**Command:**

```sh
kubectl create service clusterip my-service --tcp=80:80 --dry-run=client -o yaml
```

**Output:**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  ports:
    - port: 80
      protocol: TCP
      targetPort: 80
  selector:
    app: my-service
  type: ClusterIP
```

#### Creating a ConfigMap

A ConfigMap is an API object used to store non-confidential data in key-value pairs.

**Command:**

```sh
kubectl create configmap my-config --from-literal=key1=value1 --dry-run=client -o yaml
```

**Output:**

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  key1: value1
```

#### Creating a Secret

A Secret is an API object that stores sensitive data such as passwords, OAuth tokens, and SSH keys.

**Command:**

```sh
kubectl create secret generic my-secret --from-literal=username=admin --from-literal=password=secret --dry-run=client -o yaml
```

**Output:**

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  password: c2VjcmV0
  username: YWRtaW4=
```

#### Creating a Namespace

A Namespace is a way to divide cluster resources between multiple users.

**Command:**

```sh
kubectl create namespace my-namespace --dry-run=client -o yaml
```

**Output:**

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: my-namespace
```

### 4. Applying the Generated Manifests

Once you have generated the manifest files, you can apply them to your cluster using the `kubectl apply` command:

```sh
kubectl apply -f <manifest-file.yaml>
```

### 5. Additional Options

- **Labels:**
  You can add labels to resources during creation.

  **Command:**

  ```sh
  kubectl create deployment my-deployment --image=myimage --dry-run=client -o yaml --labels="env=production,app=myapp"
  ```

  **Output:**

  ```yaml
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: my-deployment
    labels:
      app: myapp
      env: production
  spec:
    replicas: 1
    selector:
      matchLabels:
        app: my-deployment
    template:
      metadata:
        labels:
          app: my-deployment
      spec:
        containers:
          - name: my-deployment
            image: myimage
  ```

- **Annotations:**
  You can also add annotations to resources.

  **Command:**

  ```sh
  kubectl create deployment my-deployment --image=myimage --dry-run=client -o yaml --annotations="description='My deployment'"
  ```

  **Output:**

  ```yaml
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: my-deployment
    annotations:
      description: "My deployment"
  spec:
    replicas: 1
    selector:
      matchLabels:
        app: my-deployment
    template:
      metadata:
        labels:
          app: my-deployment
      spec:
        containers:
          - name: my-deployment
            image: myimage
  ```

### Conclusion

The `kubectl create` command is a versatile tool for creating and managing Kubernetes resources. By using the `--dry-run=client -o yaml` options, you can generate YAML manifest files for various resource types, which can then be applied to your cluster using `kubectl apply`. Understanding how to create, manage, and customize these manifest files is essential for effective Kubernetes resource management.

---

### This is the output of `kubectl create --help`

```sh
Create a resource from a file or from stdin.

 JSON and YAML formats are accepted.

Examples:
  # Create a pod using the data in pod.json
  kubectl create -f ./pod.json

  # Create a pod based on the JSON passed into stdin
  cat pod.json | kubectl create -f -

  # Edit the data in registry.yaml in JSON then create the resource using the edited data
  kubectl create -f registry.yaml --edit -o json

Available Commands:
  clusterrole           Create a cluster role
  clusterrolebinding    Create a cluster role binding for a particular cluster role
  configmap             Create a config map from a local file, directory or literal value
  cronjob               Create a cron job with the specified name
  deployment            Create a deployment with the specified name
  ingress               Create an ingress with the specified name
  job                   Create a job with the specified name
  namespace             Create a namespace with the specified name
  poddisruptionbudget   Create a pod disruption budget with the specified name
  priorityclass         Create a priority class with the specified name
  quota                 Create a quota with the specified name
  role                  Create a role with single rule
  rolebinding           Create a role binding for a particular role or cluster role
  secret                Create a secret using a specified subcommand
  service               Create a service using a specified subcommand
  serviceaccount        Create a service account with the specified name
  token                 Request a service account token

Options:
    --allow-missing-template-keys=true:
        If true, ignore any errors in templates when a field or map key is missing in the
        template. Only applies to golang and jsonpath output formats.

    --dry-run='none':
        Must be "none", "server", or "client". If client strategy, only print the object that
        would be sent, without sending it. If server strategy, submit server-side request without
        persisting the resource.

    --edit=false:
        Edit the API resource before creating

    --field-manager='kubectl-create':
        Name of the manager used to track field ownership.

    -f, --filename=[]:
        Filename, directory, or URL to files to use to create the resource

    -k, --kustomize='':
        Process the kustomization directory. This flag can't be used together with -f or -R.

    -o, --output='':
        Output format. One of: (json, yaml, name, go-template, go-template-file, template,
        templatefile, jsonpath, jsonpath-as-json, jsonpath-file).

    --raw='':
        Raw URI to POST to the server.  Uses the transport specified by the kubeconfig file.

    -R, --recursive=false:
        Process the directory used in -f, --filename recursively. Useful when you want to manage
        related manifests organized within the same directory.

    --save-config=false:
        If true, the configuration of current object will be saved in its annotation. Otherwise,
        the annotation will be unchanged. This flag is useful when you want to perform kubectl
        apply on this object in the future.

    -l, --selector='':
        Selector (label query) to filter on, supports '=', '==', and '!='.(e.g. -l
        key1=value1,key2=value2). Matching objects must satisfy all of the specified label
        constraints.

    --show-managed-fields=false:
        If true, keep the managedFields when printing objects in JSON or YAML format.

    --template='':
        Template string or path to template file to use when -o=go-template, -o=go-template-file.
        The template format is golang templates
        [http://golang.org/pkg/text/template/#pkg-overview].

    --validate='strict':
        Must be one of: strict (or true), warn, ignore (or false).              "true" or "strict" will use a
        schema to validate the input and fail the request if invalid. It will perform server side
        validation if ServerSideFieldValidation is enabled on the api-server, but will fall back
        to less reliable client-side validation if not.                 "warn" will warn about unknown or
        duplicate fields without blocking the request if server-side field validation is enabled
        on the API server, and behave as "ignore" otherwise.            "false" or "ignore" will not
        perform any schema validation, silently dropping any unknown or duplicate fields.

    --windows-line-endings=false:
        Only relevant if --edit=true. Defaults to the line ending native to your platform.

Usage:
  kubectl create -f FILENAME [options]

Use "kubectl create <command> --help" for more information about a given command.
Use "kubectl options" for a list of global command-line options (applies to all commands).
```
