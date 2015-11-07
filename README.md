This project aims to make it easy to spin up a vulnerable webapplication environment for pentesting. I will say I didn't create anything new, just a way to use Vagrant to build these up.

Many of the applications come directly from the OWASP-BWA project.

The webgoat ansible configuration was originally taken from Trane9991/WebGoat-Ansible

Most of the Vagrant/Ansible install and configuration came from the geerlingguy/drupal-vm project

It should take 5-10 minutes to build or rebuild the VM from scratch on a decent broadband connection.

## Quick Start Guide

This Quick Start Guide will help you quickly build the brokenWebApps VM.

### 1 - Install dependencies (VirtualBox and Vagrant)

  1. Download and install [VirtualBox](https://www.virtualbox.org/wiki/Downloads) 
  2. Download and install [Vagrant](http://www.vagrantup.com/downloads.html).

Note for Faster Provisioning (Mac/Linux only): *[Install Ansible](http://docs.ansible.com/intro_installation.html) on your host machine, so Drupal VM can run the provisioning steps locally instead of inside the VM.*

Note for Linux users: *If NFS is not already installed on your host, you will need to install it to use the default NFS synced folder configuration. See guides for [Debian/Ubuntu](https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nfs-mount-on-ubuntu-14-04), [Arch](https://wiki.archlinux.org/index.php/NFS#Installation), and [RHEL/CentOS](https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nfs-mount-on-centos-6).*

Note on versions: *Please make sure you're running the latest stable version of Vagrant, VirtualBox, and Ansible, as the current version of this VM is tested with the latest releases. As of August 2015: Vagrant 1.7.4, VirtualBox 5.0.2, and Ansible 1.9.2.*

### 2 - Build the Virtual Machine

  1. Download this project and put it wherever you want.
  2. Open Terminal, cd to this directory (containing the `Vagrantfile` and this README file).
  3. Type in `vagrant up`, and let Vagrant do its magic.

If you have Ansible installed on your host machine: Run `$ sudo ansible-galaxy install -r provisioning/requirements.yml --force` prior to step 3 (`vagrant up`), otherwise Ansible will complain about missing roles.

Note: *If there are any errors during the course of running `vagrant up`, and it drops you back to your command prompt, just run `vagrant provision` to continue building the VM from where you left off. If there are still errors after doing this a few times, post an issue to this project's issue queue on GitHub with the error.*

### 3 - Configure your host machine to access the VM.

  1. [Edit your hosts file](http://www.rackspace.com/knowledge_center/article/how-do-i-modify-my-hosts-file), adding the line `192.168.88.88  brokenWebApps.dev` so you can connect to the VM.
    - You can have Vagrant automatically configure your hosts file if you install the `hostsupdater` plugin (`vagrant plugin install vagrant-hostsupdater`). All hosts defined in `apache_vhosts` or `nginx_hosts` will be automatically managed.
    - You can also have Vagrant automatically assign an available IP address to your VM if you install the `auto_network` plugin (`vagrant plugin install vagrant-auto_network`), and set `vagrant_ip` to `0.0.0.0` inside `config.yml`.
  2. Open your browser and access [http://brokenWebApps.dev/](http://brokenWebApps.dev/). The default login for the admin account is `admin` for both the username and password.

## Other Notes

  - To shut down the virtual machine, enter `vagrant halt` in the Terminal in the same folder that has the `Vagrantfile`. To destroy it completely (if you want to save a little disk space, or want to rebuild it from scratch with `vagrant up` again), type in `vagrant destroy`.

## License

This project is licensed under the MIT open source license.

## Many Many thanks to the following:

[Jeff Geerling](http://jeffgeerling.com/) - This project shamelessly rips off much of the work Jeff did in the [DrupalVM](http://drupalvm.com) project.

[Trane9991](https://github.com/Trane9991) - For the WebGoat ansible configurations
