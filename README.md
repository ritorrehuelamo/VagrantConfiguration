# Vagrant Configuration
Vagrant machine for web dev

## Node.JS configuration

``` ruby
Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.synced_folder ".", "/var/www/project"
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
