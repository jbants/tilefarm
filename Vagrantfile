
# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'rbconfig'
is_windows = (RbConfig::CONFIG['host_os'] =~ /mswin|mingw|cygwin/)

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.network :private_network, ip: "192.168.33.15"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--name", "ALCES_tileserver", "--memory", "1024"]
  end

  # Shared folder from the host machine to the guest machine. Uncomment the line
  # below to enable it.
	if is_windows
	  # Provisioning configuration for shell script.
	  config.vm.provision "shell" do |sh|
	    sh.path = "provisioning/JJG-Ansible-Windows/windows.sh"
	    sh.args = "provisioning/vagrant.yml"
	  end
	else
	  config.vm.provision "ansible" do |ansible|
	    ansible.playbook = "provisioning/vagrant.yml"
	    ansible.host_key_checking = false
	    ansible.verbose = "v"
	  end
	end
end