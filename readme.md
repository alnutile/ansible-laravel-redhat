# Ansible and CenotOS 7 / RedHat 7 and Laravel

# Some links that helped save the day

## CentOS and PHP Fpm
https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-centos-7

## PHP 5.6 this one took over 
http://www.if-not-true-then-false.com/2011/install-nginx-php-fpm-on-fedora-centos-red-hat-rhel/

## Nginx and CentOS
https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-server-blocks-on-centos-7

## SSL 
https://www.digitalocean.com/community/tutorials/how-to-create-a-ssl-certificate-on-nginx-for-centos-6

## Overview Of Using Ansible
https://serversforhackers.com/an-ansible-tutorial

## Tools

### Linting
http://www.yamllint.com/

## Setting up Centos Vagrant box

ansible-playbook --limit local -s centos.yml -u centos -k --ask-sudo-pass --extra-vars "user=centos"

To the request so it will not hang at Gathering data


Still might need more work

  1) Locks at gethering data cause I need to setup sudo to ask first for password then it might work


## Setting up Nginx on the servers

`cd server_config/ansible`

### Local VM
ansible-playbook --limit local -s nginx.yml -u centos --extra-vars "user=centos version=centos"

### Stage
ansible-playbook --limit serverstage -s nginx.yml -u ec2-user --extra-vars "user=ec2-user version=rhel"

### Prod
ansible-playbook --limit serverprod -s nginx.yml -u meta-data-tool --extra-vars "user=ec2-user version=rhel"

## FAQ

Where are the logs!

check /var/log/nginx/default-error.log as sudo su

BadGateway

Check /var/run/php-fpm/php-fpm.sock make sure it is read writable by the user of the system and the group nginx