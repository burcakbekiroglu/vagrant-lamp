# Vagrant LAMP #

This is a catch-all LAMP stack provisioned with Ansible to be used on test scripts, small projects or projects that do require their own virtual machine.

## Quick Setup ##

Quick setup using pre-build custom images hosted on [Atlas](https://atlas.hashicorp.com/scottjs) cloud.

### Images ###

Available pre-build images that can be used for WordPress and Laravel, etc.

* `scottjs/centos7-apache-mariadb-php56` - LAMP with PHP 5.6
* `scottjs/centos7-apache-mariadb-php71` - LAMP with PHP 7.1

### Setup ###

1. Download a copy of this repository to a location of your choice
2. Copy, paste and rename `Vagrantfile-sample` to `Vagrantfile`
3. Uncomment `config.vm.box` for the image you want to use
4. Update settings as required such as IP address and memory
5. Uncomment one of the synced folder options (either NFS or normal) and update the path to your projects
	* Choose NFS mode for more speed but less compatibility
	* Choose normal mode for less speed but more compatibility
6. Update `config.vm.synced_folder` to point to the location of your projects
7. Run `vagrant up` from the project root folder.

### Usage ###

Make sure you have a host entry set up for the IP you have configured.

The virtual machine uses a catch-all virtual host mechanism. 

If you have a project located in:

`/Users/<username>/Projects/mywebsite/public`

The web address can be either:

`http://mywebsite.public.development.dev`
`http://mywebsite.local.dev`

This assumes that your configured Vagrantfile synced folder is:

`/Users/<username>/Projects`

All website files that you want accessible must be located in `public` subfolder. 

### MySQL ###

MariaDB is installed with a default database set up if you want to run your database within the VM. The username, password and default database is `vagrant`. You should be able to connect to it directly from your host. 

Note: destroying a VM with a database inside will also delete your database, make sure to back it.

### MailHog ###

The virtual machine is bundled with MailHog. This tool automatically catches outbound email and makes it accessible via a web interface:

`http://mywebsite.local.dev:8025`

### Performance ###

If you find the performance is slow, try switching to NFS mode and restart the VM. You can do this by finding the `config.vm.synced_folder` line in the `Vagrantfile` and comment/uncomment the line that enables NFS.

### Problems

If you have problems on your first `vagrant up` try running `vagrant reload` without any shared folders configured, let the machine fully provision then re-add the shared folder settings and restart. 

Make sure you have the [guest additions plugin](https://github.com/dotless-de/vagrant-vbguest) installed. 