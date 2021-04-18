### Task 3. Configure a remote backend

1. Create a Cloud Storage bucket resource inside the `storage` module. For the bucket name, use your **Project ID**.

**Steps** -
Add the following code to the `modules/storage/storage.tf` file:
Replace the `<Enter your Project ID>` with your project Id
```
resource "google_storage_bucket" "storage-bucket" {
  name          = <Enter your Project ID>
  location      = "US"
  force_destroy = true
  uniform_bucket_level_access = true
}
```

2. Add the module reference to the `main.tf` file.

**Steps** -
Add the follwoing code in the `main.tf` file:
```
module "storage" {
  source     = "./modules/storage"
}
```
Run the following commands -

```
terraform init
terraform apply
```

3. Configure this storage bucket as the remote backend inside the `main.tf` file. Be sure to use the prefix `terraform/state` so it can be graded successfully.

**Steps** -
update the following code in `main.tf` file:

```
terraform {
  backend "gcs" {
    bucket  = "<FILL IN PROJECT ID>"
 prefix  = "terraform/state"
  }
  required_providers {
    google = {
      source = "hashicorp/google"
      version = "3.55.0"
    }
  }
}
```
Run the command `terraform init`

4. If you've written the configuration correctly, upon apply, Terraform will ask whether you want to copy the existing state data to the new backend. Type yes at the prompt.

**Steps** -

Run the command `terraform apply`
Type `yes` at the prompt
