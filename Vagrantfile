# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "private_network", ip: "192.168.2.10"
  config.vm.synced_folder "./", "/ansible-openstack"

  config.vm.hostname = "controller.example.com"
  config.hostmanager.enabled = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true

  # if Vagrant.has_plugin?("vagrant-proxyconf")
  #   config.proxy.http     = "http://proxy-server.example.com:8080"
  #   config.proxy.https    = "http://proxy-server.example.com:8080"
  #   config.proxy.no_proxy = "localhost,127.0.0.1,.example.com"
  # end

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
    vb.cpus = 2
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y libffi-dev libssl-dev python-dev python python-pip
    sudo pip install ansible netaddr
    sudo ansible-galaxy install ericsysmin.chrony
    sudo ansible-galaxy install geerlingguy.mysql
    sudo ansible-galaxy install Stouts.rabbitmq
  SHELL

end
