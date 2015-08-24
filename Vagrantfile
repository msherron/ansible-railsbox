# -*- mode: ruby -*-
# vi: set ft=ruby :

# Use config.yml for basic VM configuration.
require 'yaml'
dir = File.dirname(File.expand_path(__FILE__))
if !File.exist?("#{dir}/config.yml")
  raise 'Configuration file not found! Please copy example.config.yml to config.yml and try again.'
end
vconfig = YAML::load_file("#{dir}/config.yml")

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8888

  config.vm.hostname = vconfig['vagrant_hostname']
  if vconfig['vagrant_ip'] == "0.0.0.0" && Vagrant.has_plugin?("vagrant-auto_network")
    config.vm.network :private_network, :ip => vconfig['vagrant_ip'], :auto_network => true
  else
    config.vm.network :private_network, ip: vconfig['vagrant_ip']
  end
  config.ssh.insert_key = false
  config.ssh.forward_agent = true

  config.vm.box = vconfig['vagrant_box']

  for synced_folder in vconfig['vagrant_synced_folders'];
    config.vm.synced_folder synced_folder['local_path'], synced_folder['destination'],
      type: synced_folder['type'],
      rsync__auto: "true",
      rsync__exclude: synced_folder['excluded_paths'],
      rsync__args: ["--verbose", "--archive", "--delete", "-z", "--chmod=ugo=rwX"],
      id: synced_folder['id'],
      create: synced_folder.include?('create') ? synced_folder['create'] : false,
      mount_options: synced_folder.include?('mount_options') ? synced_folder['mount_options'] : []
  end

  # Setup the box.
  config.vm.provision :ansible do |ansible|
    ansible.playbook = "setup.yml"
  end

  # Set the name of the VM. See: http://stackoverflow.com/a/17864388/100134
  config.vm.define vconfig['vagrant_machine_name'] do |d|
  end

end
