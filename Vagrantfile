# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.
  config.vagrant.plugins = "vagrant-timezone"

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "debian/bookworm64"
  config.vm.box_version = "12.20250126.1"
  config.vm.hostname = "omv-dev"

  if Vagrant.has_plugin?("vagrant-timezone")
    config.timezone.value = "Europe/Berlin"
  end

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Make OpenMediaVault web interface available on the vagrant host.
  # Use http://localhost:8080/ to open it.
  config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
     # Customize the resources of the virtual machine.
     # Remote development using JetBrains Gateway works
     # mainly on the virtual machine, so, we shouldn't be
     # too stingy here. Development shouldn't be a torture. :-)
     vb.cpus = 8
     vb.memory = "16384"

     # Disable check for VirtualBox Guest Additions. It's being
     # installed by Debian the provider anyway and just throws
     # an warning if we don't use the exact same VirtualBox version.
     # That's okay and we want to ignore it here.
     vb.check_guest_additions = false
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "ansible_local" do |ansible|
    ansible.host_vars = {
      "default" => {
        "ansible_python_interpreter" => "auto_silent",
        "omv_version" => "sandworm",
        "use_backports_for_qemu" => false
      }
    }
    ansible.playbook = "/vagrant/provisioning/playbook.yml"
  end
end

