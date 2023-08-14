# Vagrant Ubuntu 22.04 Virtual Machine Setup

This repository contains a Vagrant configuration to create an Ubuntu 22.04 virtual machine using VirtualBox. It also includes a provisioner that performs an `apt update` and `apt upgrade` during provisioning.

## Prerequisites

Before you begin, make sure you have the following software installed on your local machine:

- [Vagrant](https://www.vagrantup.com/downloads)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

## Getting Started

1. Clone this repository to your local machine:

```
git clone https://github.com/your-username/vagrant-ubuntu-22.04.git

cd vagrant-ubuntu-22.04
```

Start the virtual machine by running:

```
vagrant up
```
Wait for Vagrant to create and provision the virtual machine. This might take a few minutes.

Once the VM is up and running, you can SSH into it using the following command:


    vagrant ssh

  You'll be logged in as the vagrant user.


## SSH Key Setup

To set up SSH key-based authentication for accessing the virtual machine, you can follow these steps:

1. **Generate SSH Key Pair**: If you want to set up SSH key authentication, you can generate an SSH key pair on your local machine using the following command:

   ```bash
   ssh-keygen -t rsa -b 4096
   ```

   Follow the prompts to create the key pair.

2. **Add Public Key to VM**: After generating the key pair, copy the contents of the public key (usually found in `~/.ssh/id_rsa.pub`) and add it to the `~/.ssh/authorized_keys` file on the virtual machine. You can do this manually or update the Vagrant provisioning script to automate this process.

3. **Access VM using SSH**: With the key pair set up, you can SSH into the VM using the private key on your local machine:

   ```bash
   ssh -i /path/to/private/key vagrant@192.168.33.10
   ```

   Replace `/path/to/private/key` with the actual path to your private key file, and `192.168.33.10` with the IP address of the virtual machine.

Remember to keep your private key secure and never share it with others.

## Customization

You can customize the Vagrant configuration by editing the Vagrantfile. Adjust the vb.memory and vb.cpus values to match your system's available resources.

## Provisioning (Optional)

If you want to customize the provisioning process, you can modify the provisioning script within the `Vagrantfile`. For example, you can install additional software or configure settings based on your needs.
