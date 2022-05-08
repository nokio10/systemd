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
box.vm.host_name = "systemd"
box.vm.provider :virtualbox do |vb|
vb.customize ["modifyvm", :id, "--memory", "2048"]
needsController = false
box.vm.provision "shell", inline: <<-SHELL
sudo cp /vagrant/watchdog /etc/sysconfig/watchdog 
sudo cp /vagrant/watchlog.service /etc/systemd/system/watchlog.service
sudo cp /vagrant/watchlog.timer /etc/systemd/system/watchlog.timer
sudo cp /vagrant/watchlog.sh /opt/watchlog.sh
sudo chmod +x /opt/watchlog.sh
sudo cp /vagrant/log /var/log/watchlog.log
sudo systemctl daemon-reload
sudo systemctl start watchlog.service
sudo systemctl start watchlog.timer
sudo cat /var/log/messages | grep Master -a2
SHELL
end
end
end
end
