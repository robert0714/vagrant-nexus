# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  if (/cygwin|mswin|mingw|bccwin|wince|emx/ =~ RUBY_PLATFORM) != nil
    config.vm.synced_folder ".", "/vagrant", mount_options: ["dmode=700,fmode=600"]
  else
    config.vm.synced_folder ".", "/vagrant"
  end
  config.vm.define "nexus-server" do |d|
    d.vm.box ="ubuntu/trusty64"
    d.vm.hostname = "nexus-server"
    d.vm.network "private_network", ip: "192.168.87.87"
#    d.vm.network "public_network", bridge: "eno4", ip: "192.168.57.89", auto_config: "false", netmask: "255.255.255.0" , gateway: "192.168.57.1"
    d.vm.provision :shell, path: "scripts/bootstrap4Ubuntu_ansible.sh"
    d.vm.provision :shell, inline: "PYTHONUNBUFFERED=1 ansible-playbook /vagrant/ansible/gitlab.yml -c local"
    d.vm.provider "virtualbox" do |v|
      v.cpus = 2
      v.memory = 2048
    end
  end   
  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end
  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = false
    config.vbguest.no_install = true
    config.vbguest.no_remote = true
  end
end
