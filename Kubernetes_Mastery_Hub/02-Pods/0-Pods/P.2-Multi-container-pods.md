# Multi-container Pods

**Description**: Design a Pod that contains multiple containers that need to work together, demonstrating inter-container communication.

## < --- In Progress --- >

Pod named "demo-2" with two containers, Nginx and Busybox. Nginx serves on port 80, and Busybox echoes a message and sleeps for an hour. Labels and annotations for organizational purposes.

```yml
apiVersion: v1
kind: Pod
metadata:
  name: demo-2
  lables:
    app: my-app
    environment: development
  annotations:
    decription: "About this multi-container project.."
spec:
  containers:
    - name: nginx-container
      image: nginx:latest
      ports:
        - containerPort: 80
    - name: busybox-container
      image: busybox:latest
      command: ["sh", "-c", "echo Hello from second container && sleep 3600"]
```
