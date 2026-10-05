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


<img width="1440" height="900" alt="Screenshot 2026-10-05 at 7 29 30 AM" src="https://github.com/user-attachments/assets/4d8dcb77-5744-44a5-ae0d-525144837819" />

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

<img width="1440" height="900" alt="Screenshot 2026-10-05 at 7 33 01 AM" src="https://github.com/user-attachments/assets/79110c2d-af66-474a-aa9a-7ed4357af513" />

## Remote State Management

Terraform state is stored remotely in Amazon S3.

```text
Bucket: jeetendra-terraform-state-2026
Path:   assignment-05/terraform.tfstate
Region: ap-south-1
```

<img width="1440" height="900" alt="Screenshot 2026-10-05 at 7 33 54 AM" src="https://github.com/user-attachments/assets/77b78843-3ca7-4995-a1c2-56e06d9db4f5" />


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
<img width="1440" height="900" alt="Screenshot 2026-10-02 at 12 39 10 AM" src="https://github.com/user-attachments/assets/aff56847-3d03-47b9-a3f4-32ab7756f97c" />


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
<img width="1440" height="900" alt="Screenshot 2026-10-02 at 12 39 10 AM" src="https://github.com/user-attachments/assets/de81018a-ce6b-466f-bcec-5a278bf10649" />


S3 state verification:

```bash
aws s3 ls s3://jeetendra-terraform-state-2026/assignment-05/
```

Output:
<img width="1440" height="900" alt="Screenshot 2026-10-05 at 7 40 06 AM" src="https://github.com/user-attachments/assets/e65e5db4-1bb2-4148-b793-4050a7da6c92" />


```text
terraform.tfstate
```

## Conclusion

This assignment demonstrates how Terraform Modules can be used to create reusable and organized AWS infrastructure. Terraform state is managed remotely using Amazon S3, with state-locking support configured for the assignment.
