# Vagrant Generic VM #

This is a generic 'catch-all' virtual machine provised with Ansible to be used on test scripts, small projects or projects that do not yet have a dedicated virtual machine config. 

### Getting set up on Mac OSX ###

* Check out the vagrant repository into a location of your choice
* Copy and paste `Vagrantfile-sample`, rename to `Vagrantfile` and update settings as required such as shared folder, IP address and memory. 
* Copy and paste `ansible/local/group_vars/all-sample.yml`, rename to `all.yml` and update settings as required, such as Apache virtualhosts.
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

### Local MySQL ###

MariaDB is installed with a default database set up if you want to run your database within the VM. The username, password and default database is `vagrant`. You should be able to connect to it directly from your host. 

Note: destroying a VM with a database inside will also delete your database, make sure to back it up regularly.

### External MySQL ###

If you want to connect to an external database located on your host (OSX/Windows), set the database hostname to be `xx.xx.xx.1`, where `xx` is to match your VM IP address. For example, if the VM address is `10.0.5.10`, then your external database connection should be `10.0.5.1`.

### Performance ###

If you find the performance of the VM is slow, try the following:

1. Try switching to NFS sync mode and restart the VM. You can do this by finding the `Synced folder` section in the `Vagrantfile`, comment out the current `config.vm.synced_folder` line and uncomment the line that enables NFS.

2. If using external MySQL, make sure you're connecting to the correct IP address mentioned above. If it's still slow, try moving the database inside the VM and change the connection to `localhost`.

Note: Laravel projects may not work properly in NFS mode.

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