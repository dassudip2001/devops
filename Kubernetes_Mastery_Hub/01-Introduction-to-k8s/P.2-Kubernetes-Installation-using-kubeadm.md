# Setting up Kubeadm - [Link](https://devopscube.com/setup-kubernetes-cluster-kubeadm/)

### What is Kubeadm?

**Kubeadm is a tool for setting up Kubernetes clusters**, keeping it simple for initial deployment and letting you build on top for more advanced configurations.

---

### System Requirements - [Link](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/#before-you-begin)

1. Host Compatibility:
   - Use a compatible Linux distribution.
2. Resources:
   - Allocate 2GB+ RAM and 2 CPUs per machine.
3. Connectivity:
   - Ensure full network connectivity between machines.
4. Unique IDs:
   - Assign unique hostname, MAC address, and product \_uuid for each node.
5. Ports:
   - Open required ports on machines.
6. Swap Configuration:
   - Follow Kubernetes version-specific swap guidelines.
   - Disable swap if kubelet isn't configured for it.

---

## Command's to run on :-

### Both Control Plane & Node

Run on both to prepare them for kubeadm.

```bash
sudo apt update
sudo swapoff -a
sudo apt install docker.io -y

sudo systemctl enable --now docker

sudo apt-get install -y apt-transport-https ca-certificates curl

curl -fsSL "https://packages.cloud.google.com/apt/doc/apt-key.gpg" | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/kubernetes-archive-keyring.gpg


echo 'deb https://packages.cloud.google.com/apt kubernetes-xenial main' | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt update
sudo apt install kubeadm=1.20.0-00 kubectl=1.20.0-00 kubelet=1.20.0-00 -y

```

---

Let's break down each line of the provided script:

1. Updates the local package database or Updates the links of packages in database.
   ```bash
   sudo apt update
   ```
2. Install necessary packages:

   - `apt-transport-https` for accessing repositories over HTTPS,
   - `ca-certificates` for SSL certificate handling, and
   - `curl` for making HTTP requests.

   ```bash
   sudo apt-get install -y apt-transport-https ca-certificates curl
   ```

3. Docker

   - Installs Docker
   - Enables and starts the Docker service using `systemd`

   ```bash
   sudo apt install docker.io -y
   sudo systemctl enable --now docker
   ```

4. GPG key

   - Downloads and saves it to the trusted keyring directory.

   ```bash
   curl -fsSL "https://packages.cloud.google.com/apt/doc/apt-key.gpg" | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/kubernetes-archive-keyring.gpg
   ```

5. Kubernetes APT repository

   - Adds the Kubernetes APT repository to the system's source list.
   - It appends a new entry specifying the repository URL and distribution (kubernetes-xenial) to a file.

   ```bash
   echo 'deb https://packages.cloud.google.com/apt kubernetes-xenial main' | sudo tee /etc/apt/sources.list.d/kubernetes.list
   ```

6. Update again, now including the newly added Kubernetes repository.

   ```bash
   sudo apt update
   ```

7. Installs specific versions (1.20.0-00) of the Kubernetes tools:

   - `kubeadm` for cluster setup and management,
   - `kubectl` for command-line interaction with the cluster, and
   - `kubelet` for handling containers on nodes.

   ```bash
   sudo apt install kubeadm=1.20.0-00 kubectl=1.20.0-00 kubelet=1.20.0-00 -y
   ```

8. Disble swap

   ```bash
   sudo swapoff -a
   ```

   - `swapoff`: This is the command used to disable swap space. Swap space is a portion of the hard drive that is used as virtual memory when the physical memory (RAM) is full.

   - `-a`: This flag with swapoff means to disable all swap devices. It's a convenient way to turn off all swap space at once.

---

### Control Plane

```bash
sudo kubeadm init

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml

sudo kubeadm token create --print-join-command
```

##### Add this if NOT on AWS or any cloud for allowing Port.

```bash
# port
sudo ufw enable
sudo ufw allow 6443
sudo ufw status
```

---

Sure, let's go through each command:

##### 1. Initializes a Kubernetes control-plane node.

```bash
sudo kubeadm init
```

- It sets up the necessary configuration and starts the Kubernetes control-plane components.
- After running this command, it provides instructions on how to join other nodes to the cluster.

##### 2. Set up local kubeconfig (both for root user and normal user):

```bash
mkdir -p $HOME/.kube
```

- Creates the `$HOME/.kube` directory if it doesn't exist.
- The `.kube` directory is the default location where Kubernetes configuration files are stored.

  ***

```bash
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
```

- Copies the Kubernetes config file for the cluster from `/etc/kubernetes/admin.conf` to the user's `$HOME/.kube/config` dir.
- This configuration file contains information about the cluster, including the server, authentication details, and more.

  ***

```bash
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

- Changes the ownership of the copied configuration file to the current user.
- It ensures that the user has the necessary permissions to use the Kubernetes configuration without requiring superuser privileges.

##### 3. Apply Weave network:

```bash
kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml
```

- This command uses `kubectl` to apply a YAML file specifying the configuration for deploying the Weave CNI (Container Network Interface) plugin.
- Weave
  : is a networking solution for Kubernetes that facilitates communication between pods in the cluster.

##### 4. Generate a token for nodes to join:

```bash
sudo kubeadm token create --print-join-command
```

- Generates a bootstrap token for authenticating nodes joining the cluster.
- The `--print-join-command` option displays the command that should be run on worker nodes to join them to the Kubernetes cluster.
- The output includes a token and the IP address or DNS name of the control-plane node.

##### 5. Expose port 6443 in the Security group for the Worker Node Only, to connect to Master Node

- please confirm in AWS, currently allowing only in master worked in VM's.

---

### Node or Worker node

##### 1. Reset the worker node:

- It resets the Kubernetes components on the worker node.

  ```bash
  sudo kubeadm reset
  ```

- If you're preparing the node for a fresh Kubernetes installation, append `pre-flight checks`.

  ```bash
  sudo kubeadm reset pre-flight checks
  ```

  ![reset]()

##### 2. Join the worker node to the cluster:

- Now need to join the worker node to the cluster using the join command you obtained from the master node.
- Additionally, you're appending `--v=5` at the end for **verbose output**, which can be helpful for troubleshooting.
- _Make sure either you are working as sudo user or use `sudo` before the command_

  ```bash
  sudo [your join command from master node] --v=5
  ```

  ![injecting token]()

  After succesful join

  ![After succesful join]()

> 1. When you append `--v=5` to a Kubernetes command, you're setting the verbosity level to 5.
> 2. This means that the system will provide a moderate amount of detailed information in its output.
> 3. The verbosity levels generally range from 0 (minimal output) to 9 (extremely detailed output). Using higher verbosity levels can be useful for troubleshooting or understanding the inner workings of a system.

---

### Verify connection of Kubernetes cluster

**On Control Plane:**

- It will display information about the nodes that are part of the cluster.

  ```bash
  kubectl get nodes
  ```

  ![img showing]()

---

### Optional: Labeling Nodes

- Node labeling in Kubernetes serves as a way to attach custom metadata to nodes.

  ```bash
  kubectl label node <node-name> node-role.kubernetes.io/cat=cat
  ```

  - `<node-name>`: Replace this with the actual name of the node you want to label.

  - `node-role.kubernetes.io/cat=cat`: This is the label being applied to the node. It follows the format `<label-key>=<label-value>`. In this case, the key is `node-role.kubernetes.io/cat`, and the value is `cat`.
  - This label suggests a custom role for the node, in this case, "cat."

---

### Optional: Test a demo Pod

- This command creates a simple demo pod named **"hello-world-pod"** using the BusyBox image.

```bash
kubectl run hello-world-pod --image=busybox --restart=Never --command -- sh -c "echo 'Hello, World' && sleep 3600"
```

- `kubectl run hello-world-pod`: This part of the command instructs Kubernetes to run a pod named "hello-world-pod."

- `--image=busybox`: Specifies the container image to use for the pod, in this case, BusyBox.

- `--restart=Never`: Sets the restart policy for the pod to **"Never"**, meaning that if the pod terminates, it will not be restarted.

- `--command -- sh -c "echo 'Hello, World' && sleep 3600"`: This part of the command specifies the command to run within the pod. In this case, it `echoes "Hello, World"` and then sleeps for 3600 seconds (1 hour).

![image]()

---

> #### Disable Swap: [NOT SURE ABOUT THIS]
>
> Kubernetes requires that swap be disabled on all nodes. You can temporarily disable it with:
>
> ```bash
> sudo swapoff -a
> ```
