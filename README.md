# Terraform Assignment 05 – Infrastructure with Terraform Modules

## Objective

The objective of this assignment is to create reusable Terraform Modules for different AWS infrastructure components and manage Terraform state using Amazon S3.

## Architecture

```text
Terraform Root Module
        |
        +-- VPC Module
        |
        +-- Subnet Module
        |
        +-- Security Group Module
        |
        +-- Instance Module
        |
        +-- AWS Infrastructure
```

## Modules Created

* **VPC Module** – Creates the VPC.
* **Subnet Module** – Creates a subnet inside the VPC.
* **Security Group Module** – Creates the security group with SSH access.
* **Instance Module** – Creates an EC2 instance.
########screenshort #########

<img width="1440" height="900" alt="Screenshot 2026-10-05 at 7 20 42 AM" src="https://github.com/user-attachments/assets/eea73854-22ba-4999-bcfe-0ffd205c34d5" />



## Project Structure

```text
terraform-assignment-05/
├── main.tf
├── variables.tf
├── providers.tf
├── backend.tf
├── .terraform.lock.hcl
└── modules/
    ├── vpc/
    │   ├── main.tf
    │   ├── variables.tf
    │   └── outputs.tf
    ├── subnet/
    │   ├── main.tf
    │   ├── variables.tf
    │   └── outputs.tf
    ├── security-group/
    │   ├── main.tf
    │   ├── variables.tf
    │   └── outputs.tf
    └── instance/
        ├── main.tf
        ├── variables.tf
        └── outputs.tf
```

## Remote State Management

Terraform state is stored remotely in Amazon S3.

```text
Bucket: jeetendra-terraform-state-2026
Path:   assignment-05/terraform.tfstate
Region: ap-south-1
```

S3 Versioning is enabled to maintain state file versions.

A DynamoDB table was also created for Terraform state-locking support:

```text
Table: terraform-state-lock
Region: ap-south-1
Status: ACTIVE
```

## Terraform Commands Used

```bash
terraform init
terraform fmt -recursive
terraform validate
terraform plan
terraform apply
terraform state list
```

## Verification

Terraform apply completed successfully:

```text
Apply complete! Resources: 4 added, 0 changed, 0 destroyed.
```

State verification:

```bash
terraform state list
```

Output:

```text
module.instance.aws_instance.this
module.security_group.aws_security_group.this
module.subnet.aws_subnet.this
module.vpc.aws_vpc.this
```

Final plan verification:

```text
No changes. Your infrastructure matches the configuration.
```

S3 state verification:

```bash
aws s3 ls s3://jeetendra-terraform-state-2026/assignment-05/
```

Output:

```text
terraform.tfstate
```

## Conclusion

This assignment demonstrates how Terraform Modules can be used to create reusable and organized AWS infrastructure. Terraform state is managed remotely using Amazon S3, with state-locking support configured for the assignment.





