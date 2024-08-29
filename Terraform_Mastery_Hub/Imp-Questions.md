# Important Questions Module wise:

## Module 1

#### 1.1

1.  **Why is IaC Important?**

    - Discuss the significance of IaC in achieving consistency, repeatability, and scalability in infrastructure management.

2.  **Comparison with Configuration Management Tools:**

    - Explore the differences between IaC and configuration management tools (Ansible, Chef, Puppet) and when one might be more suitable than the other.

3.  **Advantages of Terraform:**

    - Discuss specific advantages of Terraform, such as its declarative syntax and multi-cloud support.

#### 1.2

1.  **Declarative vs. Imperative:**

    - Discuss the difference between declarative and imperative approaches in infrastructure provisioning, highlighting Terraform's declarative nature.

2.  **State File:**

    - Explain the concept of the Terraform state file and why it is essential for tracking the current state of the infrastructure.

3.  **Providers in Terraform:**

    - Explore the concept of providers and how they enable Terraform to work with various infrastructure platforms.

#### 1.3

1.  **AWS Services in Terraform:**

    - Discuss the significance of defining AWS resources in Terraform and how it aligns with the IaC approach.

2.  **Resource Dependencies:**

    - Explore how Terraform handles dependencies between resources, ensuring they are created in the correct order.

3.  **Dynamic vs. Static Resource Configuration:**

    - Discuss how Terraform allows dynamic configuration using variables and expressions.

---

## Module 2

#### 2.1

1.  **Importance of Variables:**

    - Discuss the role of variables in making configurations flexible and reusable.

2.  **Resource Configuration:**

    - Emphasize the significance of resources in defining the desired state of infrastructure.

3.  **Dynamic Configurations:**

    - Explore how expressions and dynamic configurations enhance the flexibility of Terraform configurations.

4.  **Advanced Features:**

    - Discuss how functions, modules, and dynamic blocks contribute to more modular and maintainable configurations.

#### 2.2

#### 2.3

1.  **Provider Versioning:**

    - Discuss the importance of specifying provider versions in larger projects to maintain compatibility.

2.  **Provider Configuration Options:**

    - Explore additional configuration options available for providers, such as `alias` and `allowed_account_ids`.

3.  **Authentication Best Practices:**

    - Discuss best practices for managing credentials, such as using environment variables or credential files.

---

## Module 3

#### 3.1

1.  **Importance of `terraform init`:**

    - Discuss why `terraform init` is a necessary step before applying any Terraform configuration.

2.  **Plugin Versioning:**

    - Explain the significance of specifying provider versions to ensure consistency across runs.

3.  **Backend Initialization:**

    - Discuss scenarios where a backend may need to be initialized and how it impacts state management.

#### 3.2

1.  **Benefits of File Separation:**

    - Discuss why separating configurations into distinct files enhances readability and maintenance.

2.  **Variables in Terraform:**

    - Explain the role of variables in making configurations more dynamic and adaptable.

3.  **Data Sources:**

    - Discuss scenarios where data sources are useful, especially for fetching information from external systems.

#### 3.3

1.  **Pros and Cons of Local State:**

    - Discuss the advantages and disadvantages of using local state in different scenarios.

2.  **Remote State Best Practices:**

    - Explore best practices for configuring and using remote state, including security considerations.

3.  **Changing State Backends:**

    - Discuss scenarios where changing the state backend might be necessary and the considerations involved.

#### 3.4

---
