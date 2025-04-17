## Creating an Azure Resource Group using Terraform

Create a directory and navigate to it
```bash
cd mkdir rg-lab && cd rg-lab
```

Open a new file named resource-group.tf for editing:

```bash
vi resource-group.tf
```
Press INSERT(i) to enter insert mode and add the following content:

```hcl
provider "azurerm" {
  features {}
  resource_provider_registrations = "none"
  subscription_id = "b70f2b66-b08e-4775-8273-89d81847a0c2" ## Update subscription_id with yours
}

resource "azurerm_resource_group" "RG" {
  name     = "tf-resource-grp"
  location = "East US"
}
```
Press ESCAPE and type :wq! to save and close the file.

Initialize the working directory using the following command:
```
terraform init
```
Plan the execution to preview changes Terraform will make:
```
terraform plan
```
Apply the changes to create the resource group:
```
terraform apply
```
Run the following command or visit the Azure portal to confirm that the resource group has been created:
```
az group list -o table
```
Once verified, clean up the resources to avoid incurring charges:
```
terraform destroy
```
Navigate back to the home directory and delete the folder:
```
cd ~ && rm -rf rg-lab
```
