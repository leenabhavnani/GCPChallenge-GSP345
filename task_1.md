### Task 1. Create the configuration files

1. In Cloud Shell, create your Terraform configuration files and a directory structure that resembles the following:
```
main.tf
variables.tf
modules/
└── instances
    ├── instances.tf
    ├── outputs.tf
    └── variables.tf
└── storage
    ├── storage.tf
    ├── outputs.tf
    └── variables.tf
  ```  
 **Steps** -
 ```
 touch main.tf
 touch variables.tf
 mkdir modules
 cd modules
 mkdir instances
 mkdir storage
 cd instances
 touch instances.tf
 touch outputs.tf
 touch variables.tf
 cd ../storage
 touch storage.tf
 touch outputs.tf
 touch variables.tf
  ```
  
2. Fill out the variables.tf files in the root directory and within the modules. Add three variables to each file: region, zone, and project_id. For their default values, use us-central1, us-central1-a, and your Google Cloud Project ID.

**Steps** - Add the below code in the 3 variables.tf file
```
variable "region" {
 default = "us-central1"
}

variable "zone" {
 default = "us-central1-a"
}

variable "project_id" {
 default = "<FILL IN PROJECT ID>"
}
```
3. Add the Terraform block and the Google Provider to the main.tf file.

**Steps** - Add the below lines in main.tf

```
terraform {
  required_providers {
    google = {
      source = "hashicorp/google"
      version = "3.55.0"
    }
  }
}
provider "google" {
  project     = var.project_id
  region      = var.region
  zone        = var.zone
}
module "instances" {

  source     = "./modules/instances"

}
```

Run `terraform init` in Cloud Shell in the root directory to initialize terraform
