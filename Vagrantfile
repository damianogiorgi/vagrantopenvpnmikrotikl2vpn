# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  config.vm.box = "geerlingguy/centos7"

  config.vm.define "gw1" do |subconfig|
    subconfig.vm.hostname = "gw1"

    # Link betweek gateways
    subconfig.vm.network :private_network, ip: "192.168.200.1", virtualbox__intnet: "gwnetwork"
    subconfig.vm.network :private_network, ip: "192.168.201.1", virtualbox__intnet: "mikrotik1"

    subconfig.vm.provision "shell", inline: <<-SHELL
    sudo /vagrant/ovpn-config/scripts/requirements.sh
    sudo /vagrant/ovpn-config/scripts/gw1-easyrsa.sh
    sudo /vagrant/ovpn-config/scripts/openvpnconf.sh gw1
    SHELL

  end

  config.vm.define "gw2" do |subconfig|
    subconfig.vm.hostname = "gw2"

    # Link betweek gateways
    subconfig.vm.network :private_network, ip: "192.168.200.2", virtualbox__intnet: "gwnetwork"
    subconfig.vm.network :private_network, ip: "192.168.202.1", virtualbox__intnet: "mikrotik2"

    subconfig.vm.provision "shell", inline: <<-SHELL
    sudo /vagrant/ovpn-config/scripts/requirements.sh
    sudo /vagrant/ovpn-config/scripts/gw2-easyrsa.sh
    sudo /vagrant/ovpn-config/scripts/openvpnconf.sh gw2
    SHELL
  end

  config.vm.define "mikrotik1" do |subconfig|

    subconfig.vm.network "private_network", virtualbox__intnet: "mikrotik1", auto_config: false
    subconfig.vm.network "private_network", virtualbox__intnet: "client1", auto_config: false
    subconfig.vm.box = "cheretbe/routeros"
    subconfig.vm.provider "virtualbox" do |virtualbox|
      virtualbox.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
      virtualbox.customize ["modifyvm", :id, "--nicpromisc3", "allow-all"]
      virtualbox.customize ["modifyvm", :id, "--nicpromisc4", "allow-all"]
    end
  end

  config.vm.define "mikrotik2" do |subconfig|

    subconfig.vm.network "private_network", virtualbox__intnet: "mikrotik2", auto_config: false
    subconfig.vm.network "private_network", virtualbox__intnet: "client2", auto_config: false
    subconfig.vm.box = "cheretbe/routeros"
    subconfig.vm.provider "virtualbox" do |virtualbox|
      virtualbox.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
      virtualbox.customize ["modifyvm", :id, "--nicpromisc3", "allow-all"]
      virtualbox.customize ["modifyvm", :id, "--nicpromisc4", "allow-all"]
    end
  end



  config.vm.define "client1" do |subconfig|
    subconfig.vm.hostname = "client1"
    subconfig.vm.network :private_network, ip: "192.168.100.10", virtualbox__intnet: "client1"
  end

  config.vm.define "client2" do |subconfig|
    subconfig.vm.hostname = "client2"
    subconfig.vm.network :private_network, ip: "192.168.100.20", virtualbox__intnet: "client2"
  end

  # config.vm.define "client3" do |subconfig|
  #   subconfig.vm.hostname = "client3"
  #   subconfig.vm.network :private_network, ip: "192.168.101.10", virtualbox__intnet: "client3"
  # end


  # config.vm.define "client4" do |subconfig|
  #   subconfig.vm.hostname = "client4"
  #   subconfig.vm.network :private_network, ip: "192.168.101.20", virtualbox__intnet: "client4"
  # end

  # config.vm.define "client5" do |subconfig|
  #   subconfig.vm.hostname = "client5"
  #   subconfig.vm.network :private_network, ip: "192.168.102.10", virtualbox__intnet: "client5"
  # end

  # config.vm.define "client6" do |subconfig|
  #   subconfig.vm.hostname = "client6"
  #   subconfig.vm.network :private_network, ip: "192.168.102.20", virtualbox__intnet: "client6"
  # end

end
