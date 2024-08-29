# Terraform Mastery Hub <img src="./Img/terraform-logo.png" width="35">

# < --- In Progress --- >

Learn Terraform with this comprehensive learning repository, delving into in-depth tutorials and practical insights.

# Terraform Learning Syllabus

### Prerequisite

- HCL Learning repo
- AWS CLI

### **Module 1: Introduction to Terraform and AWS**

- **[1.1 Understanding Infrastructure as Code (IaC)](./Module-01/1.1-Understanding-IaC.md)**

  - Understand the concept of IaC and its benefits.
  - Explore different IaC tools and why Terraform is widely adopted.

- **[1.2 Introduction to Terraform & Installing](./Module-01/1.2-Installing-Terraform.md)**

  - Overview of Terraform as a declarative infrastructure provisioning tool.
  - Installation and basic configuration.

- **[1.3 AWS Fundamentals](./Module-01/1.3-AWS-Funda.md)**

  - Understanding key AWS services used in infrastructure provisioning.
  - Overview of AWS Resource Types.

- **[1.4 Different Types of Treeaform files](./Module-01/1.4-Different-Types-Treeaform-files.md)**

  - Understanding key AWS services used in infrastructure provisioning.
  - Overview of AWS Resource Types.

### **Module 2: Terraform Basics**

- **[2.1 HCL Recap](./Module-02/2.1-HCL-Recap.md)**

  - Brief overview for those who already know HCL syntax.
  - Advanced HCL features.

- **[2.2 Terraform Workspaces](./Module-02/2.2-Workspace.md)**

  - Managing multiple environments with Terraform workspaces.
  - Best practices for environment-specific configurations.

- **[2.3 Terraform `required_providers` and `providers`](./Module-02/2.3-Providers.md)**

  - Understanding and configuring the AWS provider.
  - Managing multiple providers in a single configuration.

**Practical Exercise**

- [P.2.1 Terraform Workspaces in a Multi-Environment Setup](./Module-02/P.2.1-Workspaces-Multi-Environment.md)

### **Module 3: Terraform Workflow**

- **[3.1 Initializing a Terraform Configuration `terraform init`](./Module-03/3.1-Initializing-Configuration.md)**

  - `terraform init` command and its significance.
  - Managing provider plugins.

- **[3.2 Structuring Terraform Configurations](./Module-03/3.2-Structuring-Configurations.md)**

  - Structuring Terraform configurations for readability and reusability.
  - Using variables and data sources.

- **[3.3 State Management](./Module-03/3.3-State-Management.md)**

  - Importance of Terraform state.
  - Remote and local state management.

- **[3.4 Planning `terraform plan` and Applying `terraform apply` Changes](./Module-03/3.4-Planning-Applying-Changes.md)**

  - `terraform plan` and `terraform apply` commands.
  - Understanding and reviewing execution plans.

**Practical Exercise**

- [P.3.1 Creating and Writing to a Text File using Terraform](./Module-03/P.3.1-Creating-Writing-Text-File.md)

- [P.3.2 Provisioning NGINX with Docker on Linux](./Module-03/P.3.2-Provisioning-NGINX-Docker.md)

### **Module 4: Managing AWS Resources**

- **4.1 EC2 Instances**

  - Creating and managing EC2 instances with Terraform.
  - Advanced configuration options.

- **4.2 Networking with Terraform**

  - VPCs, subnets, and security groups.
  - Leveraging AWS networking services.

- **4.3 AWS IAM and Security**

  - Managing IAM roles and policies.
  - Implementing security best practices with Terraform.

### **Module 5: Advanced Terraform Concepts**

- **5.1 Dynamic Blocks and Expressions**

  - Utilizing dynamic blocks for flexibility.
  - Advanced use of expressions in Terraform.

- **5.2 Input and Output Variables**

  - Managing input variables for reusability.
  - Output variables and their significance.

### **Module 6: Terraform and AWS Best Practices**

- **6.1 Infrastructure Testing**

  - Introduction to testing infrastructure code.
  - Implementing unit tests for Terraform configurations.

- **6.2 GitOps and Version Control**

  - Leveraging version control for infrastructure as code.
  - Implementing GitOps workflows with Terraform.

- **6.3 Continuous Integration and Deployment (CI/CD) with Terraform**

  - Integrating Terraform with CI/CD pipelines.
  - Automating the deployment of infrastructure changes.

**Module 7: Monitoring and Troubleshooting**

- **7.1 Logging and Monitoring**

  - Implementing logging for Terraform executions.
  - Utilizing AWS CloudWatch for monitoring.

- **7.2 Troubleshooting Terraform Issues**

  - Common errors and debugging techniques.
  - Strategies for handling state file issues.

**Module 8: Security and Compliance**

- **8.1 Infrastructure Compliance as Code**

  - Implementing compliance checks with Terraform.
  - Tools and best practices for security automation.

- **8.2 Secrets Management**

  - Integrating Terraform with AWS Secrets Manager.
  - Secure handling of sensitive information.

**Module 9: Real-world Use Cases and Best Practices**

- **9.1 Multi-Tier Application Deployment**

  - Deploying a multi-tier application using Terraform.
  - Best practices for scaling and managing complex infrastructures.

- **9.2 Migration Strategies with Terraform**

  - Strategies for migrating existing infrastructure to Terraform.
  - Case studies and real-world examples.

**Module 10: Project Work and Capstone**

- **10.1 Final Project**

  - Applying all learned concepts in a real-world scenario.
  - Individual or group project based on a provided use case.

- **10.2 Capstone Presentation**

  - Presenting the final project to the class.
  - Feedback and discussion on implementation choices.
