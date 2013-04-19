# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::Config.run do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.customize ["modifyvm", :id, "--memory", "512"]

  # This is only necessary if your CPU does not support VT-x or you run virtualbox
  # inside virtualbox
  config.vm.customize ["modifyvm", :id, "--vtxvpid", "off"]

  # You can adjust this to the amount of CPUs your system has available
  config.vm.customize ["modifyvm", :id, "--cpus", "1"]

  # Configure network interface
  config.vm.network :hostonly, "192.168.0.10"

  # Forward guest port 80 to host port 4567
  config.vm.forward_port 80, 4567
  config.vm.forward_port 8080, 4668

  # NFS shared folders
  config.vm.share_folder "share", "/var/www/", "www", :nfs => true

  config.vm.provision :ansible do |ansible|
    ansible.inventory = "ansible_hosts"
    ansible.playbook = "provision.yml"
  end

end
