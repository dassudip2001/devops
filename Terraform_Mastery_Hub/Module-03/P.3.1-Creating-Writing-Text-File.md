# Creating and Writing to a Text File using Terraform

# Provisioning NGINX with Docker on Linux

## Task

1.  **Directory Setup:**

    - Create a new directory for your Terraform project with an appropriate name.

2.  **Configuration File:**

    - Inside the directory, create a Terraform configuration file named `main.tf` using a text editor.

3.  **Terraform Resource:**

    - Define a Terraform resource of type `local_file` named "my_file" in the `main.tf` file.
    - Set the filename to "abc.txt" and provide the content as "Learning Abc."

4.  **Initialization and Execution:**

    - Initialize the Terraform configuration to prepare for execution.
    - Apply the Terraform configuration to create the text file and write the specified content.

5.  **Verification:**

    - After applying the configuration, verify that a file named `abc.txt` is created in the current directory.
    - Manually inspect the contents of the file to ensure it matches the specified content.

6.  **Infrastructure Cleanup:**

    - Once verification is complete, execute the necessary Terraform command to destroy the infrastructure and remove the created text file.

## Solution

#### **Step 1: Setup**

No Installation need because **local** provider is avilable to terraform by default.

#### **Step 2: Create a Terraform Configuration with Docker Provider**

1.  Make a new dir and `main.tf` file for your Terraform project.

    ```bash
    mkdir my_terraform_project
    cd my_terraform_project
    ```

    ```bash
    touch main.tf
    ```

2.  Open `main.tf` with your text editor and write Terraform configuration using the **local** provider (its avilable to terraform).

```hcl
resource "local_file" "my_file" {
  filename = "abc.txt"
  content  = "Where is my nibbi."
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

#### **Step 4: Check files**

- After Terraform applies the configuration.

- File named, `abc.txt` should be created.

#### **Step 5: Destroy the Infrastructure**

Use the following command to destroy the infrastructure:

```bash
terraform destroy
```

---
