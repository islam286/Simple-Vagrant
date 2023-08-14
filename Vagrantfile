# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/22.04"
  
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 4096
    vb.cpus = 2
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt update
    sudo apt upgrade -y
    
    # SSH provisioning commented out
    # Generate SSH key pair
    # ssh-keygen -t rsa -b 4096 -f /home/vagrant/.ssh/id_rsa -N ""
    
    # Copy public key to authorized_keys
    # mkdir -p /home/vagrant/.ssh
    # cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
    # chmod 600 /home/vagrant/.ssh/authorized_keys
    # chmod 700 /home/vagrant/.ssh
    # chown -R vagrant:vagrant /home/vagrant/.ssh
  SHELL
end

