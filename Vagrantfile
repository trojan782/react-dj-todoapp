# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |vb|
    vb.cpus = 2
    vb.memory = "1024"
  end

  config.vm.define "frontend", primary: true, autostart: false do |frontend|
    frontend.vm.box = "ubuntu/trusty64"
    frontend.vm.synced_folder ".", "/vagrant"
    frontend.vm.hostname = "frontend.local"
    frontend.vm.network "private_network", ip: "192.168.56.1", hostname:true
    frontend.vm.network "forwarded_port", guest: 8081, host: 8081
    frontend.vm.provision "shell", path: "provision/ansible_install.sh"
    frontend.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "provision/frontend.yml"
    end
  end

  config.vm.define "backend", primary: true, autostart: false do |backend|
    backend.vm.box = "ubuntu/trusty64"
    backend.vm.synced_folder ".", "/vagrant/backend"
    backend.vm.network "private_network", ip: "192.168.56.2"
    backend.vm.network "forwarded_port", guest: 8888, host: 8888
    backend.vm.provision "shell", path: "/provision/ansible_install.sh"
    backend.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "provision/backend.yml"
    end
  end
end
