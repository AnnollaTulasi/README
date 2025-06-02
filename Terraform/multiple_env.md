- tfvars
- workspaces
- seperate codebase

**tfVars**
* it is better to have seperate buckets and dynamotables
* and these will be called in backend.tf
```
dev
    backend.tf
    dev.tfvars
prod
    backend.tf
```
- in the above backend.tf we mention the bucket and dynamodb details
- if we give terraform.tfvars as the file name the values will be picked from here
- if we don't mention the file name as terraform.tfvars we have to explicitly mention
```
terraform init --backend-config=dev/backend.tf
terraform plan -var-file=dev/dev.tfvars
```
- Usually tfvars are ignored in gitignorefile we should comment them

**Terraform Workspaces**
- we have terraform.workspace variable which actually has the value of workspace which is pointed
- **lookup** : from map it will retrieve particular key's value
- instead of we creating different buckets and locks in s3,terraform workspace creates a env and based on environment they are categorized differently
```
lookup('var.instance_type','terraform.workspace')
```
```
terraform workspace new <worspce_name> //used to create new worspaces
terraform workspace list
terraform workspace select prod
```
