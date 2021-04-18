### Task 6. Use a module from the Registry

1. In the Terraform Registry, browse to the Network Module.

2. Add this module to your main.tf file. Use the following configurations:

    * Use version 2.5.0 (different versions might cause compatibility errors).

    * Name the VPC terraform-vpc, and use a global routing mode.

    * Specify 2 subnets in the us-central1 region, and name them subnet-01 and subnet-02.

    * You do not need any secondary ranges or routes associated with this VPC, so you can omit them from the configuration.

**Steps** -

Add the following code in the `main.tf`

```
module "vpc" {
    source  = "terraform-google-modules/network/google"
    version = "~> 2.5.0"

    project_id   = var.project_id
    network_name = "terraform-vpc"
    routing_mode = "GLOBAL"

    subnets = [
        {
            subnet_name           = "subnet-01"
            subnet_ip             = "10.10.10.0/24"
            subnet_region         = "us-central1"
        },
        {
            subnet_name           = "subnet-02"
            subnet_ip             = "10.10.20.0/24"
            subnet_region         = "us-central1"
            subnet_private_access = "true"
            subnet_flow_logs      = "true"
            description           = "This subnet has a description"
        }
    ]
}
```
Run the following commands and type `yes` when prompted

```
terraform init
terraform apply
```

3. Navigate to the instances module and update the configuration resources to connect tf-instance-1 to subnet-01 and tf-instance-2 to subnet-02.

**Steps** -

Enter the following code inside the `network_interface` in the `modules/instances/instances.tf `

For tf-instance-1 -
Replace
```
 network_interface {
 network = "default"
  }
  ```
  with 
```
network_interface {
 network = "terraform-vpc"
    subnetwork = "subnet-01"
  }
 ```
 For tf-instance-2 -
 Replace
 ```
  network_interface {
 network = "default"
  }
  ```
  with
```
network_interface {
 network = "terraform-vpc"
    subnetwork = "subnet-02"
  }
 ```
Run the following commands and type `yes` when prompted

```
terraform init
terraform apply
```
 
