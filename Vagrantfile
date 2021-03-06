# -*- mode: ruby -*-
# vi: set ft=ruby :
# 

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
VAGRANTFILE_API_VERSION = "2"

# CPU and RAM can be adjusted depending on your system
CPUCOUNT = "2"
RAM = "4096"


$provision = <<SCRIPT
rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

yum -y install python-pip git python2-boto \
                python-netaddr python-httplib2 python-devel \
                gcc libffi-devel openssl-devel python2-boto3 \
                python-click python-six pyOpenSSL httpd-tools \
                java-1.8.0-openjdk-headless python-passlib \
                docker docker-compose

# Startup docker

systemctl start docker

# Fix memory issue for es
sysctl -w vm.max_map_count=262144  

mkdir -p /usr/share/realtime-monitor
cd /usr/share/realtime-monitor

git clone https://github.com/nearform/stats.git 
git clone https://github.com/nearform/stats-to-elasticsearch.git
git clone https://github.com/nearform/create-stats-dashboard.git
git clone https://github.com/nearform/slow-rest-api.git

# Clone repository
cd /usr/share/realtime-monitor/slow-rest-api
git checkout stats-demo
cd stats-demo
docker-compose  build --no-cache
docker-compose up





SCRIPT

$shell= <<SCRIPT

curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash
source ~/.bashrc

nvm install node

# install node tools
npm i -g autocannon
npm i -g @nearform/create-stats-dashboard
npm i -g concurrently


# After login, change to openshift-ansible-aws directory


SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "centos/7"
  
  config.vm.provider "virtualbox" do |v|
    v.memory = "#{RAM}"
    v.cpus = "#{CPUCOUNT}"
  end
  
  config.vm.synced_folder "./", "/vagrant", disabled: true
  config.vm.network "forwarded_port", guest: 5601, host: 5601 # kibana
  config.vm.network "forwarded_port", guest: 9200, host: 9200 # elasticsearch
  config.vm.network "forwarded_port", guest: 9300, host: 9300 # elasticsearch
  config.vm.provision "shell", inline: $provision
  config.vm.provision "shell", inline: $shell, privileged: false

end