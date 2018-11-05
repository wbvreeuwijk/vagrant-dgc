# vagrant-dgc
Building Collibra DGC images using Vagrant / Packer

# Using vagrant to build a DGC Box

## Prerequisits

There are a number of components needed to get this to work
1. VirtualBox (Available at https://www.virtualbox.org/wiki/Downloads)
1. Vagrant (Installation instructions at: https://www.vagrantup.com/intro/getting-started/install.html)
1. Collibra DGC installer (To be downloaded here: [dgc-linux-5.5.1-FINAL.sh](https://ds2ov5mdb7moj.cloudfront.net/551%20files/dgc-linux-5.5.1-FINAL.sh) )
1. The contents of this repository

## Process

After VirtualBox and Vagrant have been installed and downloaded start a command prompt and type

`vagrant version`

This should return the version information op vagrant (version 2.2.0 as of this writing). Now we need to create a directory to store the vagrant files in. Create a directory, enter that directory and perform the vagrant initialisation.

```Shell
mkdir vagrant-dgc
cd vagrant-dgc
vagrant init
```

Now we need to add the contents of the repository into this directory
- Vagrantfile
- collibra-config.json

The collibra-config.json contains a number of settings for setting up the Collibra instance.

Finally place the Collibra installer (*dgc-linux-5.5.1-FINAL.sh*) in that same directory and start the VM build process by issueing the `vagrant up` command.

