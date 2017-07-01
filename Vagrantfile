# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<SCRIPT
sudo apt-get -y update
sudo apt-get -y install apt-transport-https ca-certificates curl software-properties-common httping
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu  $(lsb_release -cs) stable"
sudo apt-get -y update
sudo apt-get -y install docker-ce docker-compose awscli jq pssh wkhtmltopdf
sudo ln -s /usr/bin/parallel-ssh /usr/bin/pssh

sudo usermod -aG docker ubuntu

ssh-keygen -f ~/.ssh/id_rsa
git clone https://github.com/jpetazzo/orchestration-workshop.git
chmod -R 777 orchestration-workshop
cd orchestration-workshop/prepare-vms
docker-compose build
SCRIPT

# After SSH into the box, run the following:
# eval $(ssh-agent) > /dev/null
# ssh-add

Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/xenial64"
    config.vm.hostname = "dockertraining"
    config.vm.network :private_network, ip: "192.168.3.10"
    config.hostsupdater.aliases = ["dockertraining.app"]
    config.vm.synced_folder ".", "/var/www/public", :mount_options => ["dmode=777", "fmode=666"]
    config.vm.provision "shell", inline: $script
end
