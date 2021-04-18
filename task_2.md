### Task 2. Import infrastructure

1. In the Google Cloud Console, on the **Navigation menu**, click **Compute Engine > VM Instances**. Two instances named **tf-instance-1** and **tf-instance-2** were already created for you.

**Steps** -
Navigate to Compute Engine > VM Instances. Click on tf-instance-1. Copy the Instance ID.
Navigate to Compute Engine > VM Instances. Click on tf-instance-2. Copy the Instance ID.

2. Import the existing instances into the instances module.

To do this, you will need to:

* Write the resource configuration to match the pre-existing instances.
* Add the module reference into the main.tf file.
* Use the terraform import command to import them into your instances module.

**Steps** -
Update the `instances.tf` file

vi modules/instances/instances.tf      or nano modules/instances/instances.tf

```
resource "google_compute_instance" "tf-instance-1" {
  name         = "tf-instance-1"
  machine_type = "n1-standard-1"
  zone         = var.zone

  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-10"
    }
  }
  
  network_interface {
 network = "default"
  }
}

resource "google_compute_instance" "tf-instance-2" {
  name         = "tf-instance-2"
  machine_type = "n1-standard-1"
  zone         = var.zone

  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-10"
    }
  }

  network_interface {
 network = "default"
  }
}
```
Run the following command to import the first instance and replace the `<INSTANCE-ID>` with the id of tf-instance-1.

`terraform import module.instances.google_compute_instance.tf-instance-1 <INSTANCE-ID>`

Run the following command to import the second instance and replace the `<INSTANCE-ID>` with the id of tf-instance-2.

`terraform import module.instances.google_compute_instance.tf-instance-2 <INSTANCE-ID>`

Once the instances are imported, run the following commands -
```
terraform plan
terraform apply
```
Type **yes** at the dialogue after you run the apply command to accept the state changes.
