## Steps for terraform

Make main.tf with provider info --> Terraform init (This will install the provider) --> Terraform plan (To see everything would be okay) --> Terraform apply

Terraform.tfstate --> Holding state of current infrastructure..

Post that, terraform destroy for destroying the infrastructure..

## Variables

Post terraform apply..

terraform apply -var "instance_name=YetAnotherName"

**This way you can make the variables as dynamic and overriding the default instance name by passing in a variable using the -var flag.
Terraform will update the instance's Name tag with the new name. Respond to the confirmation prompt with yes.**

## Terraform output : Query data with outputs

Terraform prints output values to the screen when you apply your configuration. Query the outputs with the terraform output command.

```terraform
 terraform output
instance_id = "i-0bf954919ed765de1"
instance_public_ip = "54.186.202.254"
```
