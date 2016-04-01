# Vagrant Generic VM #

This is a generic 'catch-all' virtual machine to be used on test scripts, small projects or projects that do not yet have a dedicated virtual machine config. 

### How do I get set up? ###

* Check out the repository into project folder or location of your choice
* Copy and paste config-sample.yaml, rename to config.yaml and update as required.
* At a minimum, please check line 35 (synced folder path) and line 103 (vhosts)
* Run `vagrant up` from the project root foler

### Usage ###

Make sure you have a host entry set up for `192.168.56.100`, or the IP address you have configured for the machine. 

The virtual machine uses a 'catch-all' virtual host mechanism. 

If you have a project located in:

`/Users/<username>/Projects/mywebsite/public`

The web address for that website will be:

`http://mywebsite.public.development.dev`

This assumes that your configured synced folder is:

`/Users/<username>/Projects`

All website files that you want accessible must be located in `public` subfolder. 

### Automatic DNS ###

For Mac OS X users, you can avoid having to update host entries by using a program called Dnsmasq, which can be set up to automatically map *.development.dev to the IP address of your machine.

For information here:

https://passingcuriosity.com/2013/dnsmasq-dev-osx/