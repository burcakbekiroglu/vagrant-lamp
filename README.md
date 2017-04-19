# Vagrant LAMP #

This is a catch-all LAMP stack provised with Ansible to be used on test scripts, small projects or projects that do require their own virtual machine.

### Getting set up ###

* Check out the vagrant repository into a location of your choice
* Copy and paste `Vagrantfile-sample`, rename to `Vagrantfile`
* Update settings as required such as IP address and memory
* Uncomment one of the shared folder options (either NFS or normal) and update the path to your projects. 
	* Choose NFS mode for more speed but less compatibility
	* Choose normal mode for less speed but more compatibility
* Run `vagrant up` from the project root folder.

### Problems

If you have problems on your first `vagrant up` try running `vagrant reload` without any shared folders configured, let the machine fully provision then re-add the shared folder settings and restart. 

Make sure you have the [guest additions plugin](https://github.com/dotless-de/vagrant-vbguest) installed. 

### Windows ###

For windows, set the shared path syntax looks like this:

`C:/Users/myusername/Development/Websites`

Change to match your environment.

Note: the Ansible provisioner doesn't work on Windows but you can use a [pre-built base box](https://atlas.hashicorp.com/scottjs/boxes/centos7-apache-mariadb-php) instead. 

### Usage ###

Make sure you have a host entry set up for the IP you have configured.

The virtual machine uses a catch-all virtual host mechanism. 

If you have a project located in:

`/Users/<username>/Projects/mywebsite/public`

The web address will be either:

`http://mywebsite.public.development.dev`

`http://mywebsite.local.dev`

This assumes that your configured Vagrantfile synced folder is:

`/Users/<username>/Projects`

All website files that you want accessible must be located in `public` subfolder. 

### Local MySQL ###

MariaDB is installed with a default database set up if you want to run your database within the VM. The username, password and default database is `vagrant`. You should be able to connect to it directly from your host. 

Note: destroying a VM with a database inside will also delete your database, make sure to back it.

### External MySQL ###

If you want to connect to an external database located on your host (OSX/Windows), set the database hostname to be `xx.xx.xx.1`, where `xx` is to match your VM IP address. For example, if the VM address is `10.0.5.10`, then your external database connection should be `10.0.5.1`.

### Performance ###

If you find the performance of the VM is slow, try the following:

1. Try switching to NFS sync mode and restart the VM. You can do this by finding the `Synced folder` section in the `Vagrantfile`, comment out the current `config.vm.synced_folder` line and uncomment the line that enables NFS.

2. If using external MySQL, make sure you're connecting to the correct IP address mentioned above. If it's still slow, try moving the database inside the VM and change the connection to `localhost`.

Note: Laravel projects may not work properly in NFS mode.

### MailHog ###

The virtual machine is bundled with MailHog. This tool automatically catches outbound email and makes it accessible via a web interface:

`http://mywebsite.local.dev:8025`

or 

`http://10.0.0.10:8025`