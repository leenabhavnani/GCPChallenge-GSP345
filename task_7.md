### Task 7. Configure a firewall

1. Create a firewall rule resource in the main.tf file, and name it tf-firewall. This firewall rule should permit the terraform-vpc network to allow ingress connections on all IP ranges (0.0.0.0/0) on TCP port 80.

**Steps** -

Add the following lines in the main.tf and replce the <PROJECT_ID> with current Project Id

```
resource "google_compute_firewall" "tf-firewall" {
  name    = "tf-firewall"
 network = "projects/<PROJECT_ID>/global/networks/terraform-vpc"

  allow {
    protocol = "tcp"
    ports    = ["80"]
  }

  source_tags = ["web"]
  source_ranges = ["0.0.0.0/0"]
}
```

Run the following commands and enter `yes` when prompted.

```
terraform init
terraform apply
```
