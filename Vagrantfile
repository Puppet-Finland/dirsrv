# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "dirsrv" do |box|
    box.vm.box = "centos/7"
    box.vm.box_version = "1710.01"
    box.vm.hostname = "dirsrv.local"
    box.vm.network "private_network", ip: "192.168.21.100"
    box.vm.network "forwarded_port", guest: 9830, host: 19830
    box.vm.network "forwarded_port", guest: 389, host: 10389
    box.vm.synced_folder ".", "/vagrant", type: "virtualbox"
    box.vm.provision "shell" do |s|
      s.path = "vagrant/prepare.sh"
      s.args = ["-n", "dirsrv", "-f", "redhat", "-o", "el-7", "-b", "/home/vagrant"]
    end
    box.vm.provision "shell", inline: "puppet apply --modulepath /home/vagrant/modules /vagrant/vagrant/dirsrv.pp"
    box.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = 1024
    end
  end
end
