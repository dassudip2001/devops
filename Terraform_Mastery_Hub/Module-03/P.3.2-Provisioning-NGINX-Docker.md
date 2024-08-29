# Provisioning NGINX with Docker on Linux

## Task

1.  **Setup Docker:**

    - Ensure Docker is installed on your Linux machine.

2.  **Create a Terraform Configuration with Docker Provider:**

    - Establish a fresh directory for your Terraform project.
    - Inside the directory, create a file named `main.tf`.
    - Craft a Terraform configuration utilizing the Docker provider to manage the NGINX container.
    - Utilize the `docker_container` resource and appropriate settings to pull and run the NGINX container.

3.  **Initialize and Apply the Configuration:**

    - Initiate Terraform using the `terraform init` command.
    - Execute the configuration using the `terraform apply` command.

4.  **Observe NGINX Container:**

    - Post Terraform application, observe the Docker container, ensuring successful pulling and running of the NGINX image.

5.  **Note on Provisioner Usage:**

    - If applicable, confirm the execution of local-exec provisioner commands and their impact on the NGINX container.

6.  **Destroy the Infrastructure:**

    - After completing observations, utilize `terraform destroy` to meticulously clean up and halt the NGINX container.

## Solution

#### **Step 1: Setup**

Ensure Docker is installed on your Linux machine. If it's not already installed.

1. Install and Verify Docker

   ```bash
   sudo apt install docker.io -y
   ```

2. Install Terraform

   ```bash
   systemctl status docker
   ```

#### **Step 2: Create a Terraform Configuration with Docker Provider**

1.  Make a new dir and `main.tf` file for your Terraform project.

    ```bash
    mkdir my_terraform_project
    cd my_terraform_project
    ```

    ```bash
    touch main.tf
    ```

2.  Open `main.tf` with your text editor and write Terraform configuration using the Docker provider.

- **What to write..!!**
  - docker provider - Google search -> **terraform docker provider**
  - docker image - Use **Nginx**

```hcl
terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
      version = "3.0.2"
    }
  }
}


provider "docker" {}

resource "docker_image" "nginx" {
  name         = "nginx"
  keep_locally = false
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
  name  = "tutorial"

  ports {
    internal = 80
    external = 8000
  }
}
```

#### **Step 3: Initialize and Apply the Configuration**

1.  Initiate Terraform using the following command:

    ```bash
    terraform init
    ```

2.  Check the plan:

    ```bash
    terraform plan
    ```

3.  Execute the configuration using the following command:

    ```bash
    terraform apply
    ```

    - Asked to Enter Value: **yes**

#### **Step 4: Observe NGINX Container**

- After Terraform applies the configuration, observe the Docker container.
- Ensure that the NGINX container is successfully pulled and running.
- You can check this using the Docker command line or tools.

#### **Step 5: Destroy the Infrastructure**

After observing the NGINX container, use the following command to destroy the infrastructure:

```bash
terraform destroy
```

This will clean up and stop the NGINX container.

---
