# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
    vb.cpus = 2
  end

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

  config.vm.provision "python", type: "shell", preserve_order: true, inline: "echo Installing python"
  config.vm.provision "ansible", type: "shell", preserve_order: true, inline: <<-SHELL
    sudo pip install ansible netaddr
    sudo ansible-galaxy install ericsysmin.chrony
    sudo ansible-galaxy install geerlingguy.mysql
    sudo ansible-galaxy install Stouts.rabbitmq
    sudo ssh-keygen -f /root/.ssh/id_rsa -q -N ""
    sudo cat /root/.ssh/id_rsa.pub >> /root/.ssh/authorized_keys
  SHELL

  config.vm.define "ubuntu", autostart: false do |ubuntu|
    ubuntu.vm.box = "ubuntu/trusty64"
    ubuntu.vm.provision "python", type: "shell", preserve_order: true, inline: <<-SHELL
      sudo apt-get update
      sudo apt-get install -y libffi-dev libssl-dev python-dev python python-pip
    SHELL
  end

  config.vm.define "centos", autostart: false do |centos|
    centos.vm.box = "centos/7"
    centos.vm.provision "python", type: "shell", preserve_order: true, inline: <<-SHELL
      sudo yum update -y
      sudo yum install -y epel-release
      sudo yum update -y
      sudo yum install -y vim libffi-devel openssl-devel python-devel python python-pip
    SHELL
  end

end
