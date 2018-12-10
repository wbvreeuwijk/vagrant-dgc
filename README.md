# vagrant-dgc
Building Collibra DGC images using Vagrant / Packer

# Using vagrant to build a DGC Box

## Prerequisits

There are a number of components needed to get this to work
1. VirtualBox (Available at https://www.virtualbox.org/wiki/Downloads)
1. Vagrant (Installation instructions at: https://www.vagrantup.com/intro/getting-started/install.html)
1. Collibra DGC installer (To be downloaded here: [dgc-linux-5.5.1-FINAL.sh](https://ds2ov5mdb7moj.cloudfront.net/551%20files/dgc-linux-5.5.1-FINAL.sh) )
1. The contents of this repository (Download [release](https://github.com/wbvreeuwijk/vagrant-dgc/releases/download/0.1/vagrant-dgc-0.1.zip))

## Process

After VirtualBox and Vagrant have been installed and downloaded start a command prompt and type

`vagrant version`

This should return the version information op vagrant (version 2.2.0 as of this writing). Now we need to create a directory to store the vagrant files in. Create a directory, enter that directory and perform the vagrant initialisation.

```Shell
mkdir vagrant-dgc
cd vagrant-dgc
vagrant init
```

Now we need to add the following contents from the release-zip file this directory
- Vagrantfile
- collibra-config.json

The collibra-config.json contains a number of settings for setting up the Collibra instance.

Finally place the Collibra installer (*dgc-linux-5.5.1-FINAL.sh*) in that same directory and start the VM build process by issueing the `vagrant up` command. The builder will following the instructions in the Vagrantfile to build the VM. This VM uses a CentOS 7 base image. When this image is not yet available to Vagrant it will download it from its repository. Depending on you internet bandwidth this will take a few minutes. Once the process is completed there will be a line stating:

```
COMPLETED - Installation finished in ...ms.
```

You now have a running DGC VM that can be accessed through Vagrant by issueing the command 

```
vagrant ssh
```

# Using packer to build an AWS AMI

## Prerequisits

There are a number of components needed to get this to work
1. Packer installation instructions at: https://www.vagrantup.com/intro/getting-started/install.html)
1. Collibra DGC installer (To be downloaded here: [dgc-linux-5.5.1-FINAL.sh](https://ds2ov5mdb7moj.cloudfront.net/551%20files/dgc-linux-5.5.1-FINAL.sh) )
1. The contents of this repository (Download [release](https://github.com/wbvreeuwijk/vagrant-dgc/releases/download/0.1/vagrant-dgc-0.1.zip))

## Process

Check the version of packer using:

`packer version`

This should return the version information (version 1.4.0 as of this writing). ow we need to create a directory to store the packer files in. We use git to fetch the contents and create the directore

```Shell
git clone https://github.com/wbvreeuwijk/vagrant-dgc.git
cd vagrant-dgc
```

Now we need to download the Collibra installer from the Collibra community and put it in the vagrant-dgc directory. You can download the Linux installer here: https://community.collibra.com/downloads/ . CLick on the most recent version and select the main product installer for Linux (dgc-linux-*5.5.2-HOTFIX4*.sh) and put this file in the _vagrant-dgc_ directory.

Before we can start building the AMI we need the *AWS Access* Key and the *AWS Secret Key* (Read all about obtaining a AWS key-pair here: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html)

Now we can start building the AMI using the following command:

```Shell
packer build \
    -var 'aws_access_key=<AWS Access Key>' \
    -var 'aws_secret_key=<AWS Secret Key>'  \
    -var 'aws_region=<AWS Region>' \
    -var 'dgc_version=<DGC Version>' \
    collibra-aws.json
```

Example:
```Shell
packer build \
    -var 'aws_access_key=XXXXXXXXXXX' \
    -var 'aws_secret_key=XXXXXXXXXXXXXXXXXXXXXXXXXXXXX'  \
    -var 'aws_region=eu-central-1' \
    -var 'dgc_version=5.5.2-HOTFIX4' \
    collibra-aws.json
```

