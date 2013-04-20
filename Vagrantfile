# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  # VirtualBox specific configurations
  config.vm.provider "virtualbox" do |v|
    v.name = "StarterKit"
    v.customize ["modifyvm", :id, "--memory", "512"]

    # This is only necessary if your CPU does not support VT-x or you run virtualbox
    # inside virtualbox
    v.customize ["modifyvm", :id, "--vtxvpid", "off"]

    # You can adjust this to the amount of CPUs your system has available
    v.customize ["modifyvm", :id, "--cpus", "1"]
  end

  # Configure network interface
  config.vm.network :private_network, ip: "192.168.0.10"

  # Forward guest port 80 to host port 4567
  config.vm.network :forwarded_port, guest: 80, host: 4567
  config.vm.network :forwarded_port, guest: 80, host: 4668

  # NFS shared folders
  config.vm.synced_folder "./www", "/var/www", :nfs => true

  config.vm.provision :ansible do |ansible|
    ansible.inventory = "ansible_hosts"
    ansible.playbook = "provision.yml"
  end

end
