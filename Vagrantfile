
# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'rbconfig'
is_windows = (RbConfig::CONFIG['host_os'] =~ /mswin|mingw|cygwin/)

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

# Essentially use a shared folder to run the playbook from
# http://stackoverflow.com/questions/33416134/provision-vagrant-linux-vm-with-another-vagrant-linux-vm-running-ansible

$script = <<SCRIPT
sudo apt-get install -y software-properties-common
sudo apt-add-repository -y ppa:ansible/ansible
sudo apt-get update
sudo apt-get install -y ansible
ansible-playbook /home/vagrant/provisioning/vagrant.yml
SCRIPT

  config.vm.box = "ubuntu/trusty64"
  config.vm.network :private_network, ip: "192.168.33.98"
  config.vm.synced_folder "./provisioning", "/home/vagrant/provisioning"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--name", "Vagrant_test", "--memory", "1024"]
  end
	if is_windows
	  config.vm.provision "shell", inline: $script

	else
	  config.vm.provision "ansible" do |ansible|
	    ansible.playbook = "provisioning/vagrant.yml"
	    ansible.host_key_checking = false
	    ansible.verbose = "v"
	  end
	end
end