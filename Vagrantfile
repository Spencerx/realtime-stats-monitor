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


# Clone repository
mkdir -p /usr/share/stats
mkdir -p /usr/share/stats-to-elasticsearch
mkdir -p /usr/share/slow-rest-api 
mkdir -p /usr/share/create-stats-dashboard

cd /usr/share/stats
git clone https://github.com/nearform/stats.git stats

cd /usr/share/stats-to-elasticsearch
git clone https://github.com/nearform/stats-to-elasticsearch.git stats-to-elasticsearch

cd /usr/share/slow-rest-api 
git clone https://github.com/nearform/slow-rest-api.git slow-rest-api 

cd /usr/share/create-stats-dashboard
git clone https://github.com/nearform/create-stats-dashboard.git create-stats-dashboard





SCRIPT

$shell= <<SCRIPT
#mkdir -p /home/vagrant/.ssh && ssh-keygen -t rsa -N '' -f /home/vagrant/.ssh/ocp



# After login, change to openshift-ansible-aws directory
cd /usr/share

SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "centos/7"
  
  config.vm.provider "virtualbox" do |v|
    v.memory = "#{RAM}"
    v.cpus = "#{CPUCOUNT}"
  end
  
  config.vm.synced_folder "./", "/vagrant", disabled: true
  config.vm.synced_folder "./", "/usr/src/opensource-stats-demo"
  config.vm.network "forwarded_port", guest: 5601, host: 5601 # kibana
  config.vm.network "forwarded_port", guest: 5601, host: 5601 # elasticsearch
  config.vm.provision "shell", inline: $provision
  config.vm.provision "shell", inline: $shell, privileged: false

end