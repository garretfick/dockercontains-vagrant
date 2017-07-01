This repository contains a Vagrantfile that can be used to launch a
Vagrant box instance with docker configured and the docker orchestration
workshop configured.

# Creating AWS Instances

1. Start the image by executing `vagrant up`
2. SSH into the image by executing `vagrant ssh`
3. Setup SSH keys by executing the following:
```
eval $(ssh-agent) > /dev/null
ssh-add
```
4. Change directories
```
cd orchestration-workshop/prepare-vms
```
5. Set the following environment variables
```
export AWS_ACCESS_KEY_ID=<Your key>
export AWS_SECRET_ACCESS_KEY=<Your secret>
export AWS_DEFAULT_REGION=<Default region>
```
6. Finally, run the trainer script
```
./trainer start 5
```