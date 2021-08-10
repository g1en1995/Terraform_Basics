# Installation

For Windows 32/64 bit systems

1. Install terraform CLI from https://www.terraform.io/downloads.html
2. Extract the executable from the zip file and store it in a folder.
3. Add the folder path to system variables/path under envionmental variables.
4. Now open cmd and type in [$ terraform -v ] to check successful installation.

##### Install VSCode editor for easy working with Terraform. Install terraform extension by HashiCorp for syntax highlighting, formatting etc. to make your life easier.



# OverView 
### Working with AWS as the provider.
Terraform is written in a declarative configuration language known as HashiCorp Configuration Language, or optionally JSON with a .tf extension.
1. We need to define a provider. List of providers are mentioned on the terraform website. -> https://registry.terraform.io/browse/providers
    ```
    provider "aws" {
    region = "us-east-1"
    }
    ```
2. Set up authentication. Provide Access Key Id and Secret access key from security credentials in AWS.
  ```
  access_key = "***************"
  secret_key = "***************"
  ```
3. 

