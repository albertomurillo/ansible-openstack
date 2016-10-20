# -*- mode: ruby -*-
# vi: set ft=ruby :

disk = './cinder.vdi'

Vagrant.configure(2) do |config|

  config.vm.provider "virtualbox" do |vb|
    unless File.exist?(disk)
      vb.customize ['createhd', '--filename', disk, '--variant', 'Standard', '--size', 20 * 1024]
    end
    vb.memory = "6144"
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
    sudo pip install ansible netaddr shade
    sudo ansible-galaxy install ericsysmin.chrony
    sudo ansible-galaxy install geerlingguy.mysql
    sudo ansible-galaxy install Stouts.rabbitmq
    sudo ssh-keygen -f /root/.ssh/id_rsa -q -N ""
    sudo cat /root/.ssh/id_rsa.pub >> /root/.ssh/authorized_keys
  SHELL

  config.vm.define "ubuntu", autostart: false do |ubuntu|
    ubuntu.vm.box = "kaorimatz/ubuntu-16.04-amd64"
    ubuntu.vm.provider :virtualbox do |v|
      v.customize ['storageattach', :id, '--storagectl', 'IDE Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', disk]
    end
    ubuntu.vm.provision "python", type: "shell", preserve_order: true, inline: <<-SHELL
      sudo apt-get update
      sudo apt-get dist-upgrade -y
      sudo apt-get install -y libffi-dev libssl-dev python-dev python python-pip
    SHELL
  end

  config.vm.define "centos", autostart: false do |centos|
    centos.vm.box = "centos/7"
    centos.vm.provider :virtualbox do |v|
      v.customize ['storageattach', :id, '--storagectl', 'IDE', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', disk]
    end
    centos.vm.provision "python", type: "shell", preserve_order: true, inline: <<-SHELL
      sudo yum upgrade -y
      sudo yum install -y centos-release-openstack-newton
      sudo yum upgrade -y
      sudo yum install -y vim python-pip python-devel openssl-devel python-crypto python-requests
    SHELL
  end

end
