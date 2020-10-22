# ***DO NOT USE - FOR OPENLOGIC TESTING ONLY***

## Image Versions

All boxes use the latest OpenLogic cloud image for the CentOS version as of the date encoded in the release version.

_i.e. `8.2.20201021` will launch the latest OpenLogic CentOS 8.2 images on each cloud provider as of Oct 21, 2020._

## Image Variations

For this release, the AWS, Google and VirtualBox images are identical, but the Azure image is slightly different.  This is because the AWS, Google and VirtualBox images are entirely OpenLogic images whereas the Azure images are built and maintained by OpenLogic for Microsoft specifically for Azure.

The AWS and Google images include 9x5 support (email-only) from our team of Tier 4 architects and engineers.  Upon login, support details are presented on the terminal.  The Azure and VirtualBox images are not supported in this manner, but support contracts are available directly from OpenLogic.

## Image Comparison

- AWS
 - Support: OpenLogic support included
 - Fees: AWS infrastructure fees + OpenLogic image fees
- Azure
 - Support: OpenLogic support **not** included
 - Fees: Azure infrastructure fees only
- Google
 - Support: OpenLogic support included
 - Fees: Google infrastructure fees + OpenLogic image fees
- VirtualBox
 - Support: OpenLogic support **not** included
 - Fees: None (unless you have internal fees for running VirtualBox VMs)

## Configuration 

### AWS

The AWS Vagrantfile takes advantage of the [vagrant-aws](https://github.com/mitchellh/vagrant-aws) plugin and requires at least this minimum configuration:

```
  config.vm.provider :aws do |aws, override|
    aws.access_key_id = "YOUR KEY"
    aws.secret_access_key = "YOUR SECRET KEY"
    aws.session_token = "SESSION TOKEN"
    aws.keypair_name = "KEYPAIR NAME"

    aws.keypair_name = "KEYPAIR NAME"
    override.ssh.private_key_path = "/path/to/your/private_key"
  end
```

### Azure

The Azure Vagrantfile takes advantage of the [vagrant-azure](https://github.com/Azure/vagrant-azure) plugin and requires at least this minimum configuration:

```
  config.ssh.private_key_path = "/path/to/your/private_key"
  config.vm.provider :azure do |azure|

    azure.tenant_id = "AZURE_TENANT_ID"
    azure.client_id = "AZURE_CLIENT_ID"
    azure.client_secret = "AZURE_CLIENT_SECRET"
    azure.subscription_id = "AZURE_SUBSCRIPTION_ID"

    azure.vm_password = "PASSWORD"
  end
```

### Google

The Google Vagrantfile takes advantage of the [vagrant-google](https://github.com/mitchellh/vagrant-google) plugin and requires at least this minimum configuration:

```
  config.vm.provider :google do |google, override|
    google.google_project_id = "YOUR_GOOGLE_CLOUD_PROJECT_ID"
    google.google_json_key_location = "/path/to/your/google-key.json"
    
    override.ssh.username = "USERNAME"
    override.ssh.private_key_path = "/path/to/your/private_key"
  end
```

### VirtualBox

The VirtualBox Vagrantfile requires no additional plugins or configuration.
