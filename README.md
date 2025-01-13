# 2-tier application on AWS cloud using terraform
Two-tier architecture, also known as client-server architecture, is a software design pattern that divides an application into two main parts or tiers: the client tier and the server tier. Each tier has specific responsibilities and interacts with each other to provide functionality to end-users.
## Architecture

### Create S3 Backend Bucket
* Create an S3 bucket to store the .tfstate file in the remote backend.
* *Centralized Storage*: S3 provides a centralized location for storing state files, allowing multiple team members or automation tools to access the latest version of the state file. This is particularly important in collaborative environments where many people might be working on the same infrastructure.
* It is recommended to enable S3 versioning for your state file bucket. Each update to the state file will create a new version. This allows you to roll back to a previous state if necessary.
* After you apply any changes or updates to your Terraform code, the state file in the S3 backend will automatically get updated to reflect the changes in your infrastructure.
### Create a DynamoDB table for state file locking
* When using remote backends like S3, you can enable state locking via DynamoDB, preventing multiple users or processes from modifying the state at the same time. This ensures that changes to the infrastructure are made in a controlled and consistent manner.
* Give the table a name
* Make sure to add a Partition key with the name LockID and type as String.
