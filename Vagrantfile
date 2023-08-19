# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "primary" do |primary|
    primary.vm.box = "generic/ubuntu2204"
    primary.vm.network "private_network", ip: "192.168.56.3"    

    
    primary.vm.provider "virtualbox" do |vb|
      vb.memory = 4096
      vb.cpus = 2
    end

    primary.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update
      sudo apt-get upgrade -y

      # Generate SSH key pair
      ssh-keygen -t rsa -b 4096 -f /home/vagrant/.ssh/id_rsa -N ""
      
      # Copy public key to authorized_keys
      mkdir -p /home/vagrant/.ssh
      cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
      chmod 600 /home/vagrant/.ssh/authorized_keys
      chmod 700 /home/vagrant/.ssh
      chown -R vagrant:vagrant /home/vagrant/.ssh

      # # # Install and configure MySQL 8
      sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password root'
      sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root'
      sudo apt-get install -y mysql-server-8.0

      # # # Install PHP and Apache
      sudo apt-get install -y apache2 php libapache2-mod-php php-mysql

      # # # Install WordPress
      wget https://wordpress.org/latest.tar.gz
      tar -xvzf latest.tar.gz
      sudo mv wordpress /var/www/html/
      sudo chown -R www-data:www-data /var/www/html/wordpress
      sudo chmod -R 755 /var/www/html/wordpress

      # # Set up MySQL database and user for WordPress
      sudo mysql -u root -proot -e "CREATE USER 'wordpress'@'localhost' IDENTIFIED BY 'wordpress';"
      sudo mysql -u root -proot -e "GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpress'@'localhost';"
      sudo mysql -u root -proot -e "FLUSH PRIVILEGES;"
      # Set up MySQL database and user for WordPress
      sudo mysql -u root -proot -e "CREATE USER 'slave'@'%' IDENTIFIED BY 'slave';"
      sudo mysql -u root -proot -e "GRANT REPLICATION SLAVE ON *.* TO 'slave'@'%';"
      sudo mysql -u root -proot -e "FLUSH PRIVILEGES;"
      

      # # Configure Apache
      sudo a2enmod rewrite
      sudo service apache2 restart

      # # Clean up
      rm latest.tar.gz

    SHELL

    primary.vm.network "forwarded_port", guest: 80, host: 8080
    primary.vm.network "forwarded_port", guest: 3306, host: 3306

  end


end

