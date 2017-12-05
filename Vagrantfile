# Defines our Vagrant environment
#
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # create load balancer
  config.vm.define :lb do |lb_config|
      lb_config.vm.box = "ubuntu/trusty64"
      lb_config.vm.hostname = "loadbalancer"
      lb_config.vm.network :private_network, ip: "172.32.89.10"
      lb_config.vm.network "forwarded_port", guest: 80, host: 8080
      lb_config.vm.provider "virtualbox" do |vb|
        vb.memory = "512"
      end
  end

  # create some web servers
  # https://docs.vagrantup.com/v2/vagrantfile/tips.html
  (1..1).each do |i|
    config.vm.define "db#{i}" do |node|
        node.vm.box = "ubuntu/trusty64"
        node.vm.hostname = "db#{i}"
        node.vm.network :private_network, ip: "172.32.89.4#{i}"
        node.vm.network "forwarded_port", guest: 80, host: "708#{i}"
        node.vm.provider "virtualbox" do |vb|
          vb.memory = "512"
        end
    end
  end
  
  # create some web servers
  # https://docs.vagrantup.com/v2/vagrantfile/tips.html
  (1..2).each do |i|
    config.vm.define "web#{i}" do |node|
        node.vm.box = "ubuntu/trusty64"
        node.vm.hostname = "web#{i}"
        node.vm.network :private_network, ip: "172.32.89.2#{i}"
        node.vm.network "forwarded_port", guest: 80, host: "808#{i}"
        node.vm.provider "virtualbox" do |vb|
          vb.memory = "256"
        end
    end
  end

  # create some glusterfs servers
  (1..2).each do |i|
    config.vm.define "glus#{i}" do |node|
        node.vm.box = "ubuntu/trusty64"
        node.vm.hostname = "glus#{i}"
        node.vm.network :private_network, ip: "172.32.89.5#{i}"
        node.vm.network "forwarded_port", guest: 80, host: "908#{i}"
        node.vm.provider "virtualbox" do |vb|
          vb.memory = "512"
        end
    end
  end

  # create mgmt node
  config.vm.define :management do |mgmt_config|
      mgmt_config.vm.box = "ubuntu/trusty64"
      mgmt_config.vm.hostname = "management"
      mgmt_config.vm.network :private_network, ip: "172.32.89.11"
      mgmt_config.vm.provider "virtualbox" do |vb|
        vb.memory = "512"
      end
  end

end
