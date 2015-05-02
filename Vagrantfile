# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = "debian-jessie-64"
    config.vm.box_url = "http://static.gender-api.com/debian-8-jessie-rc2-x64-slim.box"

    config.vm.network :private_network, ip: "192.168.100.100"

    config.vm.synced_folder ".", "/vagrant/", :nfs => true

    config.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "1024"]
        vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        vb.customize ["modifyvm", :id, "--name", "E-vote"]
        vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/vagrant-root", "1"]
    end

    config.ssh.keep_alive = true
    config.ssh.forward_agent = true

    # Provision
    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "provision/site.yml"
        ansible.inventory_path = "provision/hosts"
    end

end
