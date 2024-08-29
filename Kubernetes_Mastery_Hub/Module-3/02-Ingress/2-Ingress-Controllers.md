# Ingress Controllers

- In order for the Ingress resource to work, the cluster must have an ingress controller running.

- It is responsible for managing Ingress resources and routing external traffic to services within the cluster.

- It acts as a traffic manager, implementing the rules defined in Ingress resources to control how incoming requests are directed to backend services.

## Why need ingress controller

The Ingress resource in Kubernetes tells traffic where to go, but the Ingress controller is the one that actually makes it happen. So, to make it work, you need both the Ingress resource and the Ingress controller.

## Purpose:

#### **Traffic Routing**:

- **Ingress controllers manage the inbound traffic to your Kubernetes cluster.**
- They route requests based on rules defined in Ingress resources, directing them to the appropriate backend services.

#### **Load Balancing**:

- Many Ingress controllers include built-in load balancing capabilities, distributing incoming traffic across multiple backend pods or services to ensure optimal performance and resource utilization.

#### **TLS Termination**:

- Ingress controllers can terminate (decrypt the) SSL/TLS encryption, allowing secure communication between clients and services within the cluster.

#### **Virtual Hosting**:

- virtual hosts allow the Ingress controller to serve multiple websites or applications on a single IP address by routing requests based on the domain name specified in the request.
- This enables efficient use of resources and simplifies management in scenarios where multiple services need to be exposed externally.

#### **Canary Deployments**:

- Some Ingress controllers support canary deployments, allowing you to direct a portion of the traffic to a new version of a service for testing purposes.

### Popular Ingress Controllers:

1.  **NGINX Ingress Controller**: NGINX Ingress Controller is one of the most widely used controllers. It's based on the popular NGINX web server and offers robust features for traffic routing, load balancing, SSL termination, and more.

2.  **Traefik**: Traefik is a modern HTTP reverse proxy and load balancer that also functions as an Ingress controller in Kubernetes. It is known for its simplicity, dynamic configuration, and integration with various orchestrators, including Kubernetes.

3.  **HAProxy Ingress**: HAProxy Ingress Controller is based on the HAProxy load balancer. It provides advanced features for traffic management and can handle high loads efficiently.

4.  **Contour**: Contour is an Ingress controller developed by VMware that uses the Envoy proxy as its data plane. It offers advanced routing capabilities and integrates well with Kubernetes.

5.  **Kong**: Kong is an open-source API gateway and Kubernetes Ingress controller. It provides features for authentication, authorization, rate limiting, and more, making it suitable for managing API traffic in Kubernetes.

### Features to Consider:

- **Compatibility**: Ensure that the Ingress controller you choose is compatible with your Kubernetes version and environment.
- **Features**: Consider the features offered by the controller, such as traffic routing options, load balancing algorithms, TLS termination capabilities, etc.
- **Performance**: Evaluate the performance and scalability of the Ingress controller, especially if you anticipate high traffic volumes.
- **Community Support**: Choose an Ingress controller with an active community and good documentation to aid in troubleshooting and support.
- **Customization**: Some controllers offer more customization options than others. Choose one that aligns with your specific requirements and use cases.

### Deployment:

- Ingress controllers are typically deployed as Kubernetes pods within the cluster.
- They may require additional configuration, such as RBAC rules, service accounts, or custom resource definitions (CRDs), depending on the controller and your environment.
- Many controllers provide **Helm charts** or manifest files to simplify the deployment process.
