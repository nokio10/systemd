# -*- mode: ruby -*-
# vim: set ft=ruby :
MACHINES = {
:systemd => {
:box_name => "centos/7",
:box_version => "2004.01",
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
sudo cp /vagrant/st1/watchdog /etc/sysconfig/watchdog 
sudo cp /vagrant/st1/watchlog.service /etc/systemd/system/watchlog.service
sudo cp /vagrant/st1/watchlog.timer /etc/systemd/system/watchlog.timer
sudo cp /vagrant/st1/watchlog.sh /opt/watchlog.sh
sudo chmod +x /opt/watchlog.sh
sudo cp /vagrant/st1/log /var/log/watchlog.log
sudo systemctl daemon-reload
sudo systemctl start watchlog.service
sudo systemctl start watchlog.timer
echo "======================================================="
echo "Результат первого задания"
sudo cat /var/log/messages | grep Master -a2
echo "======================================================="
sudo yum install epel-release -y && yum install spawn-fcgi php php-cli mod_fcgid httpd -y
sudo cp /vagrant/st2/spawn-fcgi /etc/sysconfig/spawn-fcgi
sudo cp /vagrant/st2/spawn-fcgi.service /etc/systemd/system/spawn-fcgi.service
sudo systemctl daemon-reload
sudo systemctl start spawn-fcgi
echo "======================================================="
echo "Результат второго задания"
systemctl status spawn-fcgi
echo "======================================================="
sudo cp /vagrant/st3/httpd@.service /etc/systemd/system/httpd@.service
sudo cp /vagrant/st3/httpd-first /etc/sysconfig/httpd-first
sudo cp /vagrant/st3/httpd-second /etc/sysconfig/httpd-second
sudo cp /vagrant/st3/first.conf /etc/httpd/conf/first.conf
sudo cp /vagrant/st3/second.conf /etc/httpd/conf/second.conf
sudo setenforce 0
sudo systemctl daemon-reload
sudo systemctl start httpd@first
sudo systemctl start httpd@second
echo "======================================================="
echo "Результат третьего задания"
sudo ss -tnulp | grep httpd
echo "======================================================="
SHELL
end
end
end
end
