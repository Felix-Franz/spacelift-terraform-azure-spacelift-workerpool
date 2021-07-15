# Spacelift Worker for Azure

Terraform module for deploying a Spacelift worker pool on Azure using a VMSS.

## Usage

NOTE: please make sure you [accept the terms](#accepting-terms) for our Azure Marketplace
image before trying to use the module.

```hcl
module "azure-worker" {
  source = "github.com/spacelift-io/terraform-azure-spacelift-workerpool"

  admin_password = "Super Secret Password!"

  configuration = <<-EOT
    export SPACELIFT_TOKEN="${var.worker_pool_config}"
    export SPACELIFT_POOL_PRIVATE_KEY="${var.worker_pool_private_key}"
  EOT

  location            = var.location
  resource_group_name = var.resource_group_name
  subnet_id           = var.subnet_id
  worker_pool_id      = var.worker_pool_id
}
```

## Accepting Terms

Before you can use our Marketplace image, you need to accept the terms and conditions for the
image for the subscription you want to deploy the image to. You can do this using the following
command:

```shell
az vm image terms accept \
  --publisher "spaceliftinc1625499025476" \
  --offer "spacelift_worker" \
  --plan "ubuntu_20_04"
```

More information can be found [here](https://go.microsoft.com/fwlink/?linkid=2110637).