# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
# The most common configuration options are documented and commented below.
# For a complete reference, please see the online documentation at
# https://docs.vagrantup.com.

  config.vm.box = "generic/ubuntu1804"

# Disable automatic box update checking. If you disable this, then
# boxes will only be checked for updates when the user runs
  config.vm.box_check_update = false

# Create a public network, which generally matched to bridged network.
  config.vm.network "public_network", ip: "192.168.0.97", bridge: "enp6s0"

# Set virtual machine name
  config.vm.provider "virtualbox" do |v|
    v.name = "ubu.vagrant"
  end

# Enable provisioning with a shell script. Additional provisioners such as
# Puppet, Chef, Ansible, Salt, and Docker are also available.
  
# using bash script from file to install python (needed for ansible)
  config.vm.provision :shell, :path => "install_python.sh"

# copying id_rsa.pub file from host to VM
  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/id_rsa.pub"

# using bash script to add id_rsa.pub into VM authorized_keys
  config.vm.provision "shell", inline: <<-SHELL
    cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
  SHELL

# use Ansible playbook
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
  end

end
