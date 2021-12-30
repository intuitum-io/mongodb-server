# -*- mode: ruby -*-
# vi: set ft=ruby :

BOX = "intuitum/ubuntu-server-20.04"

Vagrant.configure("2") do |config|
  
  config.vm.provider :virtualbox do |v, override|
    override.vm.synced_folder './', '/vagrant', type: 'rsync'
  end

  config.vm.define "ubuntu" do |ubuntu|
    ubuntu.vm.box = BOX
    config.disksize.size = '10GB'
    ubuntu.vm.hostname = 'mongo-server'
    ubuntu.vm.network :private_network, ip: "192.168.99.80"
    ubuntu.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 1536]
      v.customize ["modifyvm", :id, "--cpus", 1]
      v.customize ["modifyvm", :id, "--name", "mongo-server"]
    end
  end
end