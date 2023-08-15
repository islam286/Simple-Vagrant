# Vagrant Ubuntu 22.04 Virtual Machine with WordPress Setup

This repository provides a Vagrant configuration to create an Ubuntu 22.04 virtual machine using VirtualBox, along with an integrated WordPress development environment. The setup includes MySQL 8, PHP, Apache, and WordPress for streamlined web development and testing.

## Prerequisites

Before you begin, ensure you have the following software installed on your local machine:

- [Vagrant](https://www.vagrantup.com/downloads)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

## Getting Started

### 1. Clone this repository to your local machine:

```
git clone https://github.com/your-username/vagrant-ubuntu-22.04-wordpress.git

cd vagrant-ubuntu-22.04-wordpress
```

### 2. Start the virtual machine by running:

```
vagrant up
```
Wait for Vagrant to create and provision the virtual machine. This might take a few minutes.

### 3. Access the WordPress site in your web browser:

Open your web browser and navigate to: `http://localhost:8080/wordpress`
## SSH Key Setup

To set up SSH key-based authentication for accessing the virtual machine, follow these steps:

### 1. Generate SSH Key Pair: If you want SSH key authentication, generate a key pair on your local machine:


    ssh-keygen -t rsa -b 4096

### 2. Add Public Key to VM 
Copy the public key contents (usually in ~/.ssh/id_rsa.pub) and add it to ~/.ssh/authorized_keys on the VM. You can do this manually or automate it in the Vagrant provisioning script.

Access VM using SSH: SSH into the VM with the private key:


    ssh -i /path/to/private/key vagrant@192.168.33.10

Replace /path/to/private/key with the actual path to your private key and 192.168.33.10 with the VM's IP.

## Vagrant Configuration

### The Vagrantfile in this repository configures the following:

- Ubuntu 22.04 VM
- 4096MB RAM and 2 CPUs allocated to the VM
- Forwarded port: Local port 8080 -> VM port 80

## Provisioning

### The Vagrant provisioning script performs the following steps:

- Updates and upgrades the system
- Sets up SSH key pair (Optional, uncomment if needed)
- Installs MySQL 8, PHP, Apache
- Installs and sets up WordPress
- Creates MySQL user and database for WordPress
- Configures Apache for WordPress
- Cleans up temporary files

Please note that this setup is intended for local development and testing. Modify configurations for production use.
Important Notes

- MySQL root password: root
- MySQL WordPress user: Wordpress
- MySQL WordPress user password: wordpress

## Clean Up

Halt and remove the VM:

    vagrant halt
    
    vagrant destroy

## Customization

Edit the Vagrantfile to customize the VM setup, memory, and CPU allocation based on your needs.


