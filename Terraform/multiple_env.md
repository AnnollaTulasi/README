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
