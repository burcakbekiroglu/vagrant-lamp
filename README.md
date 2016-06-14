# Vagrant Generic VM #

This is a generic 'catch-all' virtual machine provised with Ansible to be used on test scripts, small projects or projects that do not yet have a dedicated virtual machine config. 

### Getting set up on Mac OSX ###

* Check out the vagrant repository into a location of your choice
* Copy and paste `Vagrantfile-sample`, rename to `Vagrantfile` and update settings as required, such as IP address and memory. 
* Copy and paste `ansible/local/group_vars/all-sample.yml`, rename to `all.yml` and update settings as required, such as Apache virtualhosts.
* Copy and paste `ansible/local/inventory-sample.yml`, rename to `inventory` and update the IP address as required.
* Run `vagrant up` from the project root folder.

### Getting set up on Windows ###

Ansible provisioning doesn't work on Windows and will have to use a pre-provisioned VM.

* Check out the vagrant repository into a location of your choice
* Download a pre-packaged copy of the VM from `\\oak\Company\Vagrant\vagrant-generic-vm@0.7.0` and place the project root folder.
* Copy and paste `Vagrantfile-packaged`, rename to `Vagrantfile` and update settings as required, such as IP address and memory.
* Run `vagrant up` from the project root folder.

### Usage ###

Make sure you have a host entry set up for `192.168.56.100`, or the IP address you have configured for the machine. 

The virtual machine uses a 'catch-all' virtual host mechanism. 

If you have a project located in:

`/Users/<username>/Projects/mywebsite/public`

The web address and host entry should be:

`http://mywebsite.public.development.dev`

This assumes that your configured Vagrantfile synced folder is:

`/Users/<username>/Projects`

All website files that you want accessible must be located in `public` subfolder. 

### Notes ###

If you change the virtual machine IP address, make sure to also update the inventory IP address within `ansible/local/inventory`

### MailHog ###

The virtual machine is bundled with MailHog. This tool automatically catches outbound email and makes it accessible via a web interface:

`http://mywebsite.public.development.dev:8025`

or 

`http://192.168.56.100:8025`

### Ansible Galaxy ###

If you want to add a new Ansible galaxy module, you can add it to:

`ansible/requirements.yml` 

and to install it, run: 

`ansible-galaxy install -r ansible/requirements.yml`

### Automatic DNS ###

For Mac OS X users, you can avoid having to update host entries by using a program called Dnsmasq, which can be set up to automatically map *.development.dev to the IP address of your machine.

For information here:

https://passingcuriosity.com/2013/dnsmasq-dev-osx/