# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.require_version ">= 1.7"

Vagrant.configure(2) do |config|

  # ===== BASE =====

  # Base box is Ubuntu 16.04 LTS (Xenial Xerus)
  # Note : we're using a commuity-powered base image as long as the Ubuntu official image
  # is broken with VirtualBox, see more at https://bugs.launchpad.net/cloud-images/+bug/1565985
  config.vm.box = "bento/ubuntu-16.04"

  # Change the VM name so that Ansible will recoignize it as a target host for provisioning
  config.vm.define "vagrantdjangobootstrap" do |foo|
  end

  # Folder sharing between the host and the guest VM
  config.vm.synced_folder ".", "/vagrant", mount_options: ["dmode=777,fmode=666"]

  # Use the default Vagrant "insecure key" to let Ansible access the VM
  config.ssh.insert_key = false

  # ===== NETWORK =====
  
  # Django (runserver mode)
  config.vm.network :forwarded_port, guest: 8000, host: 8000

  # Nginx (HTTP and HTTPS)
  config.vm.network :forwarded_port, guest: 80, host: 8080
  config.vm.network :forwarded_port, guest: 443, host: 8090

  # ===== PROVIDERS =====
  
  # VirtualBox specific configuration
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "768" # Set the amount of RAM
  end

  # ===== PROVISIONING =====

  # Ansible configuration
  config.vm.provision "ansible" do |ansible|
    ansible.playbook        = "./provision/ansible/playbook.yml"
    ansible.verbose         = "v"
    ansible.sudo            = true
    ansible.inventory_path  = "provision/ansible/inventories/vagrant"
  end

end
