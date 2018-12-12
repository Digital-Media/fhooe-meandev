# -*- mode: ruby -*-
# vi: set ft=ruby :
# vim: set et :

Vagrant.configure("2") do |config|
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # We use the original ubuntu box with ubuntu 16.04 LTS
  config.vm.box = "bento/ubuntu-16.04"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # Avoiding IP conflicts with FH network based on 10.*.*.*
  config.vm.network "private_network", ip: "192.168.7.8"

  # Mapping a folder, that can be used for WEB excercises, allowing apache running as www-data to write data to these directories
  # config.vm.synced_folder # doesn't work with npm, because links are not supported with file system vboxsf
  
  config.vm.boot_timeout = 1500

  # Configuring Image for use as web development environment
  config.vm.provision "Installing MongoDB", type: "shell",
    inline:  <<-SH
	  sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
	  echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
	  apt-get -y -qq update
	  apt-get install -y -qq mongodb-org
	  systemctl enable mongod
	SH
	
  config.vm.provision "Installing Node", type: "shell",
    inline:  <<-SH
      curl -sL https://deb.nodesource.com/setup_11.x | sudo -E bash -
      apt-get install -y -qq nodejs
	SH


	config.vm.provision "## Starting MongoDB with run: always ##", type: "shell", run: "always",
    inline: <<-SH
	  service mongod restart  && echo "MongoDB started with return code $?"   
    SH
	
	
end