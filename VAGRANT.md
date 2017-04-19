# CentOS 7 Image

This custom CentOS 7 image is bundled with common packages suitable for Laravel and WordPress local development.

## Notes

Apache web root is set using VirtualDocumentRoot to:

`/var/www/%-3/public`

If you set your shared folder in Vagrantfile to:

`config.vm.synced_folder "~/Path/To/All/Websites", "/var/www", mount_options: ["dmode=777,fmode=777"]`

With a host entry set up:

`192.168.10.10 mywebsite.local.dev`

This will automatically map to `/var/www/mywebsite` within the VM without the need for additional vhosts for 
each domain/website. 

The document root will be `/var/www/mywebsite/public`.

On the host this will be:

`~/Path/To/All/Websites/mywebsite`


## Features

The following packages are installed:

- Apache 2.4
- PHP 7.1
- MariaDB 10.1
- Composer 1.4