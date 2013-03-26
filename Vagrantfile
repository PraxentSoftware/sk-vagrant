# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'vagrant-ansible'

Vagrant::Config.run do |config|
  config.vm.box = "ubuntu1204"
  config.vm.box_url = "http://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-vagrant-amd64-disk1.box"

  config.vm.customize ["modifyvm", :id, "--memory", "512"]

  # This is only necessary if your CPU does not support VT-x or you run virtualbox
  # inside virtualbox
  config.vm.customize ["modifyvm", :id, "--vtxvpid", "off"]

  # You can adjust this to the amount of CPUs your system has available
  config.vm.customize ["modifyvm", :id, "--cpus", "1"]

  # Configure network interface
  config.vm.network :hostonly, "192.168.0.10"

  # Forward guest port 80 to host port 4567
  config.vm.forward_port 80, 1080

  # NFS shared folders
  config.vm.share_folder "share", "/var/www/", "www", :nfs => true

  config.vm.provision :ansible do |ansible|
    # point Vagrant at the location of your playbook you want to run
    ansible.playbook = "provision.yml"

    # the Vagrant VM will be put in this host group change this should
    # match the host group in your playbook you want to test
    ansible.hosts = "web-servers"
  end

end
