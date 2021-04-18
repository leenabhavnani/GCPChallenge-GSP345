### Task 5. Taint and destroy resources

1. Taint the third instance tf-instance-3, and then plan and apply your changes to to recreate it.

**Steps** -

Run the following commands -
```
terraform taint module.instances.google_compute_instance.tf-instance-3
terraform init
terraform apply
```

2. Destroy the third instance tf-instance-3 by removing the resource from the configuration file.

**Steps** -

Remove the following code from modules/instances/instance.tf

```
resource "google_compute_instance" "tf-instance-3" {
  name         = "tf-instance-3"
  machine_type = "n1-standard-2"
  zone         = var.zone
  allow_stopping_for_update = true

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
Run the following commands and type `yes` when prompted
```
terraform init
terraform apply
```
