# Vagrant Configuration
Vagrant machine for web dev

## Basic Vagrant configuration

``` ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  
  # Box settings
  config.vm.box = "ubuntu/trusty64"

  # Provider settings
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 2048
    vb.cpus = 4
  end
end


```

## Node.JS configuration

``` ruby
Vagrant.configure(2) do |config|
  # Box settings
  config.vm.box = "ubuntu/trusty64"
  # Folder settings
  config.vm.synced_folder ".", "/var/www/project"
  # Provider settings
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 2048
    vb.cpus = 4
  end
  # Node.JS shell installation
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y g++
    curl -sL https://deb.nodesource.com/setup_0.12 | sh
    apt-get install -y nodejs
    su vagrant
    mkdir /home/vagrant/node_modules
    cd /var/www/project
    ln -s /home/vagrant/node_modules/ node_modules
    npm install karma
  SHELL
end
```
