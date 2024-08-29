# Ingress

## What is Ingress?

- It is an API object
- **used** to manage **external access** to services within a cluster.
- It provides HTTP and HTTPS routing to services based on hostnames and paths.
- Ingress **sits between** the external traffic and the services running in a Kubernetes cluster, acting as a traffic controller.

<img src="../../Img/ingress.svg">

## Steps to Use Ingress:

1.  **Deploy Ingress Controller**: Before using Ingress, you need to deploy an **Ingress controller** in your Kubernetes cluster. This could be done by deploying the chosen Ingress controller's Helm chart or by using manifest files provided by the controller's documentation.

    > Only creating an Ingress resource has no effect.

2.  **Define Ingress Resource**: Create an Ingress resource that specifies the routing rules for incoming traffic. This includes hostnames, paths, and backend services.

3.  **Apply Ingress Resource**: Apply the Ingress resource to your Kubernetes cluster using `kubectl apply`.

4.  **Verify Configuration**: Ensure that the Ingress controller is correctly configured and that traffic is being routed according to the rules defined in the Ingress resource.

### Example Ingress Resource

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
    - host: example.com
      http:
        paths:
          - path: /app1
            pathType: Prefix
            backend:
              service:
                name: service1
                port:
                  number: 80
          - path: /app2
            pathType: Prefix
            backend:
              service:
                name: service2
                port:
                  number: 80
  tls:
    - hosts:
        - example.com
      secretName: example-tls-secret
```

## Ingress Class

#### **Multiple Ingress Controllers:**

- It helps to support's multiple **Ingress controllers** within a cluster.
- Each Ingress class represents a different implementation of the Ingress controller.

#### **Selective Routing:**

- With Ingress class, you can specify which Ingress controller should be responsible for managing a particular Ingress resource.
- This enables selective routing of traffic to different controllers based on the class specified in the Ingress resource.

### How to Use Ingress Class:

1.  **Define Ingress Class**: Each Ingress controller should specify its class when deployed. This is typically done through annotations in the controller's deployment manifest.

2.  **Specify Ingress Class in Ingress Resource**: When creating an Ingress resource, you can specify the desired Ingress class using the `ingressClassName` field. If no class is specified, the default class is used.

3.  **Controller Selection**: The Kubernetes API server routes the Ingress resource to the appropriate controller based on the class specified in the resource.
