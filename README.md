![OpenLogic by Perforce](https://cdn.brandfolder.io/UEOJKODA/at/pwujp1-aw3f3c-1rgw2v/logo-openlogic-tagline.png?width=600&height=189)


# ***DO NOT USE - FOR OPENLOGIC TESTING ONLY***

## Image Versions

All boxes use the latest OpenLogic cloud image for the CentOS version as of the date encoded in the release version.

_i.e. `8.2.20201022` will launch the latest OpenLogic CentOS 8.2 images on each cloud provider as of Oct 22, 2020._

## Image Variations

For this release, the AWS, Google and VirtualBox images are identical, but the Azure image is slightly different.  This is because the AWS, Google and VirtualBox images are entirely OpenLogic images whereas the Azure images are built and maintained by OpenLogic for Microsoft specifically for Azure.

The AWS and Google images include 9x5 support (email-only) from our team of Tier 4 architects and engineers.  Upon login, support details are presented on the terminal.  The Azure and VirtualBox images are not supported in this manner, but support contracts are available directly from OpenLogic.

## Image Comparison

- AWS
  - Support: OpenLogic support **included**
  - Fees: AWS infrastructure fees + OpenLogic image fees
- Azure
  - Support: OpenLogic support **_NOT_** included
  - Fees: Azure infrastructure fees only (no OpenLogic image fees)
- Google
  - Support: OpenLogic support **included**
  - Fees: Google infrastructure fees + OpenLogic image fees
- VirtualBox
  - Support: OpenLogic support **_NOT_** included
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


## Support

Included with some of our images (see the table above) is 9x5 email-only support from our team of Tier 4 architects and engineers.  

Please send support requests to support@openlogic.com including your name, email, CentOS solution name and Cloud Account ID that is running this image.

Silver (12x5) and Gold (24x7) support options are also available. 

## Next Steps

If you want to learn more about OpenLogic by Perforce, our Open Source Software support, including CentOS support, visit us at http://www.openlogic.com , email us at info@roguewave.com or call us at +1 800.487.3217
