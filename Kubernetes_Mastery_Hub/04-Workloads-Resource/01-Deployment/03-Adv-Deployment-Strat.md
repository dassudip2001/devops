# 4.1.3. Advanced Deployment Strategies

## Argo Rollouts

- Its a controller that has Custom Resource Definitions (CRDs) that extend and enhance the deployment capabilities in Kubernetes.

- It provides advanced deployment strategies, such as **blue/green deployments**, **canary deployments**, and other progressive deployment techniques.

- _Think of it as a, tool that tells how these strategies will work._

**Two notable strategies are:**

## 1. Blue-Green Deployments:

Idea
: Maintain two identical environments (blue and green). One serves live traffic (blue), while the other (green) is updated with the new version. Once the green environment is verified, traffic is switched to it.

Implementation
: Achieved by having two separate environments (Deployments) and adjusting a load balancer or service to switch traffic between them.

Benefits
: Minimal downtime, easy rollback, and the ability to test the new version in a production-like environment before redirecting traffic.

Example:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment-blue
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
    color: blue # or green
  template:
    metadata:
      labels:
        app: my-app
        color: blue # or green
    spec:
      containers:
        - name: my-container
          image: my-image
```

## 2. Canary Deployments:

Idea
: new version is first released for small group(for 20% users), if it perfoms correctly, then gradually increase the percentage of user.

Implementation
: Achieved by creating multiple Deployments with different versions and gradually shifting traffic from the old to the new version.

Benefits
: Early feedback from real users, quick detection of issues, and the ability to abort the deployment if problems arise.

Example:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment-canary
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
    version: v1 # the version
  template:
    metadata:
      labels:
        app: my-app
        version: v1
    spec:
      containers:
        - name: my-container
          image: my-image:v1
```

---

## Other Strategies

### Shadow Deployments:

Idea
: Deploy the new version alongside the existing version without directing live traffic to it. The shadow deployment only observes the behavior without affecting users.

Benefits
: Allows you to gather metrics and identify potential issues before full deployment.

### A/B Testing:

Idea
: Introduce multiple versions of a feature or a UI change and direct user traffic to different versions. Measure user engagement and performance to determine the effectiveness of each version.

Benefits
: Data-driven decision-making, understanding user preferences, and optimizing features based on real user feedback.

### Rolling Red-Black Deployments:

Idea
: Similar to blue-green deployments, but instead of maintaining two identical environments, maintain two complete sets of infrastructure (red and black). The switch between versions involves adjusting load balancer settings.

Benefits
: Like blue-green deployments, it allows for easy rollback and testing in a production-like environment.

### etc...

---

# Real-world Use Cases

Real-world scenarios where Kubernetes Deployments shows it's value:

### Real-world Use Cases

Let's explore real-world scenarios where Kubernetes Deployments shine and demonstrate their value:

#### Continuous Integration/Continuous Deployment (CI/CD):

- **Scenario:** You have a CI/CD pipeline that builds and tests your application. Using Deployments, you can automate the deployment process, ensuring a consistent and reliable rollout of your application updates.

#### High Availability and Scaling:

- **Scenario:** Your application needs to handle varying loads, and you want to ensure high availability. Deployments make it easy to scale your application by adjusting the number of replicas based on demand.

#### Zero Downtime Updates:

- **Scenario:** You need to update your application to a new version without causing downtime for your users. Deployments enable rolling updates, ensuring a smooth transition from the old version to the new one.

#### A/B Testing:

- **Scenario:** You want to perform A/B testing by deploying multiple versions of your application and directing a subset of users to each version. Deployments with service configurations allow you to control traffic routing.

#### Fault Tolerance:

- **Scenario:** In a microservices architecture, one of your services may fail. Deployments, along with ReplicaSets, ensure that failed pods are automatically replaced, maintaining the desired number of replicas.

---
