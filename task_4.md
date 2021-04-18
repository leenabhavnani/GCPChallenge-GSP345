### Task 4. Modify and update infrastructure

1. Navigate to the instances module and modify the tf-instance-1 resource to use an n1-standard-2 machine type.
2. Modify the tf-instance-2 resource to use an n1-standard-2 machine type.
3. Add a third instance resource and name it tf-instance-3. For this third resource, use an n1-standard-2 machine type.

**Steps** -

Enter the following code in `modules/instances/instances.tf` 

```
resource "google_compute_instance" "tf-instance-1" {
  name         = "tf-instance-1"
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

resource "google_compute_instance" "tf-instance-2" {
  name         = "tf-instance-2"
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
Rune the following commands and type `yes` when prompted

```
terraform init
terraform apply
```
