# Ansible Mastery Hub <img src="https://www.vectorlogo.zone/logos/ansible/ansible-icon.svg" width="35">

Ansible Learning Repository Welcome to the Ansible Learning Repository! This repository is designed to help you learn Ansible, an open-source automation tool, and enhance your skills in managing infrastructure, automating tasks, and streamlining DevOps workflows.

## Prerequisites

Before diving into this Ansible learning repository, make sure you have the following prerequisites:

- Basic understanding of Linux/Unix system administration
- Familiarity with basic programming/scripting concepts (Python is a plus)
- Previous experience with configuration management tools is beneficial but not mandatory

## Course Modules

The learning material is organized into modular structures, covering different aspects of Ansible. Each module includes sub-modules, ensuring a detailed and comprehensive learning experience.

### Module 1: Introduction to Ansible and Automation

##### [1.1 Overview of Configuration Management and Automation](./Module-1/1.1-Overview-Configuration-Management-Automation.md)

##### [1.2 Introduction to Ansible](./Module-1/1.2-Introduction-Ansible.md)

- 1.2.1 History
- 1.2.2 Architecture
- 1.2.3 Key Components

##### [1.3 Installing and Configuring Ansible](./Module-1/1.3-Installing-Configuring-Ansible.md)

##### [1.4 Inventories and Host Patterns](./Module-1/1.4-Ansible-Inventories-Host-Patterns.md)

##### [1.5 Ad-Hoc Commands](./Module-1/1.5-Ad-Hoc-Commands.md)

### Module 2: Ansible Playbooks and Roles

##### [2.1 Writing Ansible Playbooks](./Module-2/2.1-Overview-Configuration-Management-Automation.md)

- 2.1.1 Syntax
- 2.1.2 Best Practices

##### [2.2 Variables and Facts in Ansible](./Module-2/2.2-Variables-Facts-Ansible.md)

##### [2.3 Running Ansible Playbooks](./Module-2/2.3-Running-Ansible-Playbooks.md)

##### [2.4 Ansible Roles](./Module-2/2.4-Ansible-Roles.md)

- 2.3.1 Organizing Playbook Logic
- 2.3.2 Ansible Galaxy: Using and Creating Roles
- 2.3.3 Templating with **Jinja2** in Ansible

### Module 3: Ansible Modules and Handlers

##### [3.1 Ansible Modules](./Module-3/3.1-Ansible-Modules.md)

- 3.1.1 Core and Custom Modules
- 3.1.2 Managing Files, Packages, and Services with Ansible
- 3.1.3 Managing Users and Permissions

##### [3.2 Handlers](./Module-3/3.2-Handlers.md)

- 3.2.1 Triggering Actions on Changes
- 3.2.2 Error Handling and Troubleshooting in Ansible

### Module 4: Ansible Vault and Security Best Practices

##### [4.1 Ansible Vault](./Module-4/4.1-Ansible-Vault.md)

- 4.1.1 Encrypting and Securing Sensitive Data
- 4.1.2 Managing Secrets with Ansible Vault

##### [4.2 Security Best Practices for Ansible](./Module-4/4.2-Security-Best-Practices-Ansible.md)

##### [4.3 Integrating Ansible with Identity and Access Management (IAM)](./Module-4/4.3-Integrating-Ansible-Identity-IAM.md)

### Module 5: Ansible Tower and Automation Workflows

##### [5.1 Introduction to Ansible Tower](./Module-5/5.1-Introduction-Ansible-Tower.md)

##### [5.2 Installing and Configuring Ansible Tower](./Module-5/5.2-Installing-Ansible-Tower.md)

##### [5.3 Role-Based Access Control (RBAC) in Ansible Tower](./Module-5/5.3-RBAC-Ansible-Tower.md)

##### [5.4 Creating and Managing Job Templates](./Module-5/5.4-Creating-Managing-Job.md)

##### [5.5 Ansible Tower API and Automation Workflows](./Module-5/5.5-Ansible-Tower-API-Automation-Workflows.md)

### Module 6: Dynamic Inventories and Integrations

##### [6.1 Dynamic Inventories](./Module-6/6.1-Dynamic-Inventories.md)

- 6.1.1 Connecting to External Systems
- 6.1.2 Integrating Ansible with Cloud Providers (AWS, Azure, GCP)

##### [6.2 Using Ansible with Containers](./Module-6/6.2-Using-Ansible-Containers.md)

- 6.2.1 Docker
- 6.2.2 Kubernetes

##### [6.3 Continuous Integration/Continuous Deployment (CI/CD) with Ansible](./Module-6/6.3-CI-CD-with-Ansible.md)

### Module 7: Advanced Topics in Ansible

##### [7.1 Ansible and Network Automation](./Module-7/7.1-Ansible-Network-Automation.md)

##### [7.2 Ansible and Infrastructure as Code (IaC)](./Module-7/7.2-Ansible-Infrastructure-as-Code.md)

##### [7.3 Ansible and Monitoring/Logging Tools Integration](./Module-7/7.3-Ansible-Monitoring-Logging.md)

##### [7.4 Performance Tuning and Optimization in Ansible](./Module-7/7.4-Performance-Tuning-Optimization-Ansible.md)

##### [7.5 Advanced Ansible Troubleshooting](./Module-7/7.5-Advanced-Ansible-Troubleshooting.md)

### Module 8: Real-world Projects and Best Practices

##### [8.1 Case Studies](./Module-8/8.1-Case-Study.md)

- 8.1.1 Implementing Ansible in Real-world Scenarios

##### [8.2 Best Practices for Large-scale Ansible Deployments](./Module-8/8.2-Best-Practices-Large-scale-Deployments.md)

##### [8.3 Ansible Code Reviews and Collaboration](./Module-8/8.3-Ansible-Code-Reviews-Collaboration.md)

##### [8.4 Final Project:](./Module-8/8.4-Final_project.md)

- 8.4.1 Designing an Ansible Automation Solution

## Usage

This repository is self-paced, allowing you to learn Ansible at your own speed. Follow the modules in order, and complete the assignments and labs to reinforce your understanding. Feel free to experiment with the provided examples and adapt them to your specific use cases.

## Contributing

If you find any issues, have suggestions for improvement, or want to contribute additional content.

**Wanna Make Changes?**

1.  Fork the repo, create a new branch (`git checkout -b feature/your-feature-name`).
2.  Make your changes, commit (`git commit -m "Your message"`), and push (`git push origin feature/your-feature-name`).
3.  Open a pull request against `main`.

## License

This Ansible Learning Repository is licensed under the [MIT License](./LICENSE).

Happy learning!

---

1.  **Introduction to Ansible:**

    - What is Ansible and why use it?
    - Ansible architecture and components.
    - Installing and configuring Ansible.

2.  **Ansible Playbooks:**

    - Writing your first playbook.
    - Understanding YAML syntax.
    - Defining hosts and tasks.

3.  **Inventory Management:**

    - Exploring different inventory formats.
    - Dynamic inventories.

4.  **Roles in Ansible:**

    - Organizing your playbooks with roles.
    - Creating reusable and modular playbooks.

5.  **Variables and Facts:**

    - Working with variables in Ansible.
    - Ansible facts and how to use them.

6.  **Handlers:**

    - Understanding and using handlers.
    - Controlling when handlers are triggered.

7.  **Ansible Modules:**

    - Exploring commonly used Ansible modules.
    - Writing custom modules.

8.  **Working with Templates:**

    - Using Jinja2 templates in Ansible.
    - Templating best practices.

9.  **Ansible Vault:**

    - Securing sensitive data with Ansible Vault.
    - Encrypting and decrypting files.

10. **Integration with Version Control:**

    - Using Ansible with Git for version control.
    - Managing playbooks and roles in a Git repository.

11. **Advanced Ansible Topics:**

    - Ansible Tower/AWX for orchestration and automation.
    - Ansible Galaxy for sharing roles.
    - Best practices for large-scale deployments.
