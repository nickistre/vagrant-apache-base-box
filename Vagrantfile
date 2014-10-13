# -*- mode: ruby -*-
# vi: set ft=ruby :

# Custom configuration params

# How much ram for the apache box.
apache_ram = 512

# The private IP to setup the apache server as. Use this to connect to the 
# Apache vm from the host machine.
apache_private_ip = "192.168.222.10"

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define "apache", primary: true do |apache|
    # All Vagrant configuration is done here. The most common configuration
    # options are documented and commented below. For a complete reference,
    # please see the online documentation at vagrantup.com.

    # Every Vagrant virtual environment requires a box to build off of.
    apache.vm.box = "nickistre/ubuntu-trusty32-update"

    # Setup private IP port
    apache.vm.network "private_network", ip: apache_private_ip

    # Setup RAM used by vm
    apache.vm.provider "virtualbox" do |v|
      v.memory = apache_ram
    end

    # Run scripts
    # Run updates
    apache.vm.provision :shell, inline: "apt-get update -yqq && apt-get upgrade -yqq"
    # Install and setup apache2
    apache.vm.provision :shell, inline: "apt-get install -yqq apache2 && a2enmod ssl && a2ensite default-ssl.conf && service apache2 reload"
    # Do a full dist-upgrade
    apache.vm.provision :shell, inline: "apt-get dist-upgrade -yqq"
    # Cleanup apt
    apache.vm.provision :shell, inline: "apt-get autoremove -yqq && apt-get autoclean -yqq"
  end
end
