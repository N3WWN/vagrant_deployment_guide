![OpenLogic by Perforce](https://cdn.brandfolder.io/UEOJKODA/at/pwujp1-aw3f3c-1rgw2v/logo-openlogic-tagline.png?width=600&height=189)


## Image Versions

All boxes use the latest OpenLogic cloud image for the AlmaLinux version as of the date encoded in the release version.

_i.e. `9.0.v20220615` will launch the latest OpenLogic AlmaLinux 9.0 images on each cloud provider as of Jun 30, 2022._

## Image Variations

For this release, the AWS, Azure, Google and VirtualBox images will be identical when they are publicly available.  

The AWS, Azure and Google images include 9x5 support (email-only) from our team of Tier 4 architects and engineers.  Upon login, support details are presented on the terminal.  The Azure and VirtualBox images are not supported in this manner, but support contracts are available directly from OpenLogic.

## Image Comparison

- AWS
  - Support: OpenLogic support **included**
  - Fees: AWS infrastructure fees + OpenLogic image fees
  - Version: OpenLogic - AlmaLinux 9 Standard (ENA-enabled) - almalinux-9.0-v20220615
  - Marketplace: [RogueWave/OpenLogic @ AWS Marketplace](https://aws.amazon.com/marketplace/pp/prodview-ne4uq43iicvy6)
- Azure
  - Support: OpenLogic support **included**
  - Fees: Azure infrastructure fees + OpenLogic image fees
  - Version (Gen1): Perforce:AlmaLinux:9:9.0.2022061500
  - Version (Gen2): Perforce:AlmaLinux:9:9.0.2022061501
  - Marketplace: [OpenLogic @ Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?search=openlogic&page=1) (partial image list)
- Google
  - Support: OpenLogic support **included**
  - Fees: Google infrastructure fees + OpenLogic image fees
  - Version: almalinux-9-0-v20220615
  - Marketplace: [Perforce/OpenLogic @ Google Cloud Marketplace](https://console.cloud.google.com/marketplace/partners/zend-integration-public)
- VirtualBox
  - Support: OpenLogic support **_NOT_** included
  - Fees: None (unless you have internal fees for running VirtualBox VMs)
  - Version: almalinux-9-0-v20220615
- VMWare
  - Support: OpenLogic support **_NOT_** included
  - Fees: None (unless you have internal fees for running VirtualBox VMs)
  - Version: almalinux-9-0-v20220615

## Preparing your system

### Known working vagrant/plugin versions

- Vagrant
  - Vagrant 2.2.10
  - Vagrant 2.2.14
  
- vagrant-aws plugin
  - vagrant-aws 0.7.2 ([OpenLogic modified plugin](https://github.com/N3WWN/vagrant-aws/blob/master/pkg/vagrant-aws-0.7.2.gem))
- vagrant-azure plugin
  - vagrant-azure 2.0.0.pre.jeb.pre.0.2 ([OpenLogic built plugin](https://github.com/N3WWN/vagrant-azure/blob/v2.0/pkg/vagrant-azure-2.0.0.pre.jeb.pre.0.2.gem))
- vagrant-google plugin
  - vagrant-google [2.5.0](https://github.com/mitchellh/vagrant-google)

In order to be able to use all providers, install the plugins in this order: 

`vagrant-aws -> vagrant-azure -> vagrant-google`

If you only wish to use one of the providers, you do not need to use the OpenLogic modified plugins, but we recommend that you use the version(s) listed.

### Known issues with the following vagrant/plugin versions

Because of fog-google interdependencies, the stock aws and azure plugins (installed via `vagrant plugin install vagrant-aws`, for instance) do not play well together with the google plugin:

- vagrant-aws plugin
  - vagrant-aws 0.7.2 (stock plugin)
- vagrant-azure plugin
  - vagrant-azure 2.0.0 (stock plugin)
  
The stock google plugin is too old:

- vagrant-google plugin
  - vagrant-google 0.2.3 (stock plugin)

### Installing the boxes

Some providers require additional steps to install, configure or use

- VirtualBox
  - No special configuration or installation required
  - `vagrant init openlogic/almalinux-9`
  - `vagrant up --provider=virtualbox`

All others require some additional steps

**Common Steps** (choose either Vagrant Cloud, Metadata or Full URL method)

- Vagrant Cloud method
  - This method is preferred since it preserves the box version info and version checks/upgrading works
  - `vagrant box add openlogic/almalinux-9`
  - Vagrant will ask you which provider box to install... or you can specify the provider with the --provider parameter.  Example: `vagrant box add --provider=aws ./metadata-7.json`
  - `vagrant init openlogic/almalinux-9`
  - Proceed to the provider specific steps below
- Metadata method
  - This method is the next preferred since it preserves the box version info, but you must re-download the metadata file if a new box version is released, but it will contain all published versions
  - `wget https://github.com/N3WWN/vagrant_deployment_guide/raw/almalinux-9/metadata-9.json`
  - `vagrant box add ./metadata-9.json`
  - Vagrant will ask you which provider box to install... or you can specify the provider with the --provider parameter.  Example: `vagrant box add --provider=aws ./metadata-9.json`
  - `vagrant init openlogic/almalinux-9`
  - Proceed to the provider specific steps below
- Full URL method
  - This method works, but the box is always version 0 as shown in the vagrant box output: `box: Adding box 'openlogic/almalinux-9' (v0) for provider: azure`
  - `vagrant box add --name openlogic/almalinux-9 --provider aws https://app.vagrantup.com/openlogic/boxes/almalinux-9/versions/9.0.20220615/providers/aws.box`
  - `vagrant box add --name openlogic/almalinux-9 --provider azure https://app.vagrantup.com/openlogic/boxes/almalinux-9/versions/9.0.20220615/providers/azure.box`
  - `vagrant box add --name openlogic/almalinux-9 --provider google https://app.vagrantup.com/openlogic/boxes/almalinux-9/versions/9.0.20220615/providers/google.box`
  - `vagrant init openlogic/almalinux-9`
  - Proceed to the provider specific steps below

**Provider-specific Steps**

- AWS
  - Perform your chosen "All" method above
  - Edit Vagrantfile, adding the information shown in the next section for the AWS provider
  - `vagrant up --provider=aws`
- Azure
  - Perform your chosen "All" method above
  - Edit Vagrantfile, adding the information shown in the next section for the Azure provider
  - `vagrant up --provider=azure`
- Google
  - Perform your chosen "All" method above
  - Edit Vagrantfile, adding the information shown in the next section for the Google provider
  - `vagrant up --provider=google`

## Configuration

### AWS

The AWS Vagrantfile takes advantage of the [vagrant-aws](https://github.com/mitchellh/vagrant-aws) plugin and requires at least this minimum configuration:

```
  config.vm.provider :aws do |aws, override|
    aws.access_key_id = "YOUR KEY"
    aws.secret_access_key = "YOUR SECRET KEY"
    aws.session_token = "SESSION TOKEN"

    #aws.region = "REGION"
    #aws.instance_type = "TYPE"
    aws.subnet_id = "SUBNET"
    aws.keypair_name = "KEYPAIR NAME"
    override.ssh.private_key_path = "/path/to/your/private_key"
  end
```

The AWS AMI ID changes in each region.  By default, the default AMI in the box file is for region us-east-1.  If you wish to launch the instance within a different region, uncomment the `aws.region` parameter and set it appropriately.

The default instance type is t3.small (2x vCPU, 2 GB RAM) because it is available in all 16 regions (that I can see) as well as 51 of the 53 availability zones (that I can see... as of Dec 30, 2020).  

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

Additionally, the Azure Marketplace terms for the OpenLogic image need to be accepted:

PowerShell:
```
$agreementTerms=Get-AzMarketplaceterms -Publisher perforce -Product almalinux9 -Name 9
Set-AzMarketplaceTerms -Publisher perforce -Product almalinux9 -Name 9 -Terms $agreementTerms -Accept
$agreementTerms=Get-AzMarketplaceterms -Publisher perforce -Product almalinux9 -Name 9-gen2
Set-AzMarketplaceTerms -Publisher perforce -Product almalinux9 -Name 9-gen2 -Terms $agreementTerms -Accept
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

## Getting rid of the WARNING message (non-Virtualbox providers)

There is a warning message presented every time you execute a vagrant command with a cloud provider.

```
WARNING - There are Azure and OpenLogic fees associated with running this image.
  HINT: Add '$OPENLOGIC_CONFIRM="no"' to your Vagrantfile to skip this confirmation.
Enter 'Y' to continue:
```

Normally you **must** enter a single capital Y and hit enter to proceed.

If you wish to bypass this requirement, you can do it one of two ways:

1. Set and export an environment variable named `OPENLOGIC_CONFIRM` to a non-null value: `export OPENLOGIC_CONFIRM=skip`

-or-

2. Add `$OPENLOGIC_CONFIRM="no"` somewhere in your Vagrantfile

The message will be displayed as an info message without a confirmation:

```
INFO - You have accepted all Azure and OpenLogic charges associated with running this image.
```

## Support

Included with some of our images (see the table above) is 9x5 email-only support from our team of Tier 4 architects and engineers.  

Please send support requests to image-support@openlogic.com including your name, email, AlmaLinux solution name and Cloud Account ID that is running this image.

Silver (12x5) and Gold (24x7) support options are also available. 

## Next Steps

If you want to learn more about OpenLogic by Perforce, our Open Source Software support, including Enterprise Linux support, visit us at http://www.openlogic.com , email us at info@perforce.com or call us at +1 612.517.2100
