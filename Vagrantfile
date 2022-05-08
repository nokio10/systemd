# -*- mode: ruby -*-
# vim: set ft=ruby :
MACHINES = {
:systemd => {
:box_name => "centos7",
#:box_version => "2004.01",
},
}
Vagrant.configure("2") do |config|
MACHINES.each do |boxname, boxconfig|
config.vm.define boxname do |box|
box.vm.box = boxconfig[:box_name]
box.vm.box_version = boxconfig[:box_version]
box.vm.host_name = "ansible"
box.vm.provider :virtualbox do |vb|
box.vm.network "forwarded_port", guest: 22, host: 2201
box.vm.network "forwarded_port", guest: 8080, host: 8080
vb.customize ["modifyvm", :id, "--memory", "2048"]
needsController = false
box.vm.provision "shell", inline: <<-SHELL
echo "space 4 shell script"
SHELL
end
end
end
end
