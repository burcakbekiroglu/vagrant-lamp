# Creating custom base boxes

Vagrant atlas base box, instructions based on [this article](https://scotch.io/tutorials/how-to-create-a-vagrant-base-box-from-an-existing-one).

## Setup

Initial setup.

1. Run `npm install` to setup Ansible dependencies
2. Run `vagrant init centos/7`
3. Run `vagrant up`
4. Run `vagrant ssh`

## Provision

Provisioning the VM.

1. Ensure the port number matches the current virtual machine port in the `inventory` file
2. Update any configuration options such as PHP version in the `ansible-provision` folder
3. Run the Ansible provsioner:
`ansible-playbook -i ansible-provision/vagrant/inventory ansible-provision/provision.yml`

## Optimise

Optimise the box for upload.

1. Run `yum clean all`
2. Run `sudo dd if=/dev/zero of=/EMPTY bs=1M`
3. Run `sudo rm -f /EMPTY`
4. Run `cat /dev/null > ~/.bash_history && history -c && exit`

## Export

Export the box.

1. Run `vagrant package --output centos7-apache-mariadb-php71.box`
