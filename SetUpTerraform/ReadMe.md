# Installation

For Windows 32/64 bit systems

1. Install terraform CLI from https://www.terraform.io/downloads.html
2. Extract the executable from the zip file and store it in a folder.
3. Add the folder path to system variables/path under envionmental variables.
4. Now open cmd and type in [$ terraform -v ] to check successful installation.

##### Install VSCode editor for easy working with Terraform. Install terraform extension by HashiCorp for syntax highlighting, formatting etc. to make your life easier.



# OverView 
### Working with AWS as the provider.

* Terraform is an infrastructure as code (IaC) tool that allows you to build, change, and version infrastructure safely and efficiently. This includes low-level components such as compute instances, storage, and networking, as well as high-level components such as DNS entries, SaaS features, etc. Terraform can manage both existing service providers and custom in-house solutions. 
* Terraform is written in a declarative configuration language known as HashiCorp Configuration Language, or optionally JSON with a .tf extension.
* It has similar syntax no matter the provider. It is one of the main advantages points of Terraform.

### Setting up a resource
1. Create (main.tf) terraform file. We need to define a provider. List of providers are mentioned on the terraform website. -> https://registry.terraform.io/browse/providers
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
3. Provide the resource section, chosing the required services or/and instances.
   ```
   resource "aws_instance" "my_first_server" {
   ami           = "ami-#########"
   instance_type = "t2.micro"
   }
   ```
4. Initialize terraform by running the command ``` terraform init ``` from cmd in the folder where your project is localted. 
5. Next run ```terraform plan``` for dry running your execution plan before actually carrying out the actual instructions without breaking anything.
6. Run ``` terraform apply``` to carry out the required specifications from .tf file.


### Modifying a resource
1. The terraform file(main.tf) is the final plan, so whatever you modify in there will be implemented in aws console.
   For example: if you wanted to add a tag to the EC2 instance that you have created. Just add    ``` tags = {Name = "HelloWorld"} ```   in the resource
                 section and the instance created earlier will have the tag added to the instance.
                 
  So finally the your main.tf looks like 
                 
                 ```provider "aws" {
                    region = "us-east-1"
                    access_key = "################"
                    secret_key = "###########################"
                    }
                    resource "aws_instance" "my_third_server" {
                    ami           = "ami-##############"
                    instance_type = "t2.micro"

                    tags = {Name = "HelloWorld"}
                    }```

### Destroy(Delete) a resource
1. To delete the resouces just type in ``` terraform destroy ``` and the instances will get deleted.
2. Removing the resource section  and running a ```terraform apply ``` command also destroys all the instances since terraform plan is written in a declarative configuration language.

### Referenceing resource
To understand how to reference a resource in another let us take an example of creating a VPC and a subnet.
```
resource "aws_vpc" "first_vpc" {
  cidr_block       = "10.0.0.0/16"
  instance_tenancy = "default"

  tags = {
    Name = "dev_vpc"
  }
}

resource "aws_subnet" "subnet_1" {
  vpc_id     = aws_vpc.first_vpc.id
  cidr_block = "10.0.1.0/24"

  tags = {
    Name = "dev_subnet"
  }
}
```
We can reference the vpc.id in subnet creation using the name of vpc we have created.



