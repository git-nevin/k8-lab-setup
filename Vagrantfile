# encoding: utf-8
# -*- mode: ruby -*-
# vi: set ft=ruby :# Box / OS
VAGRANT_BOX = 'generic/ubuntu1804'# Memorable name for your
VM_NAME = 'k8master'# VM User — 'vagrant' by default
VM_USER = 'vagrant'# Username on your Mac
MAC_USER = 'k8master'# Host folder to sync
HOST_PATH = 'D://vm//' + VM_NAME
# Where to sync to on Guest — 'vagrant' is the default user name
GUEST_PATH = '/home/' + VM_USER + '/' + VM_NAME
# # VM Port — uncomment this to use NAT instead of DHCP
# VM_PORT = 8080
Vagrant.configure(2) do |config|  # Vagrant box from Hashicorp
  config.vm.box = VAGRANT_BOX
  # Actual machine name
  config.vm.hostname = VM_NAME  # Set VM name in Virtualbox
  config.vm.box = "generic/ubuntu1804"
  config.vm.box_check_update = false
  config.vm.provider "virtualbox" do |v|
    v.name = VM_NAME
    v.memory = 2548	
  end  
  #DHCP — comment this out if planning on using NAT instead
  
  config.vm.network "private_network", type: "dhcp"  
  # # Port forwarding — uncomment this to use NAT instead of DHCP
  # config.vm.network "forwarded_port", guest: 80, host: VM_PORT  
  # Sync folder
  config.vm.synced_folder HOST_PATH, GUEST_PATH  
  # Disable default Vagrant folder, use a unique path per project
  config.vm.synced_folder '.', '/home/'+VM_USER+'', disabled: true  
  # Install Git, Node.js 6.x.x, Latest npm
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
    apt-get install -y build-essential
    apt-get update
    apt-get install -y curl
    curl -fsSL https://get.docker.com -o get-docker.sh
    sudo sh get-docker.sh
    apt-get upgrade -y
    apt-get autoremove -y
  SHELL
end
