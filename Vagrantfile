# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |vb|
    vb.cpus = 4
    vb.memory = "1024"
  end

  config.vm.define "frontend" primary: true autostart: false do |frontend|
    frontend.vm.box = "ubuntu/trusty64"
    frontend.vm.synced_folder = ".", "/vagrant"
    frontend.vm.hostname = "frontend"
    frontend.vm.network "private_network", ip: "192.168.56.1"
    frontend.vm.network "forwarded_port" guest: 8081 host: 8081
    frontend.vm.provision "shell", path: "provision/ansible_install.sh"
    frontend.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "/to_be_added"
    end
  end

  config.vm.define "backend" primary: true autostart: true do |backend|
    backend.vm.box = "ubuntu/trusty64"
    backend.vm.synced_folder = ".", "/vagrant/backend"
    backend.vm.network "private_network", ip: "192.168.56.2"
    backend.vm.network "forwarded_port" guest: 8888 host: 8888
    backend.vm.provision "shell", path: "/provision/ansible_install.sh"
    backend.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "/to_be_added"
    end
  end
end
