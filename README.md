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



