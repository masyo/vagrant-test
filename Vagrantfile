# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.ssh.username = "root"

  config.vm.define :test_vm do |test_vm|
    test_vm.vm.box = "centos64"
    test_vm.vm.network :private_network, :libvirt__network_name => 'muldernet'
  end
  
  config.vm.provider :libvirt do |libvirt|
    libvirt.driver = "qemu"
    libvirt.host = "localhost"
    libvirt.connect_via_ssh = true
    libvirt.username = "root"
    libvirt.storage_pool_name = "default"
  end

  config.vm.provision "chef_client" do |chef|
    chef.chef_server_url = "https://192.168.100.154:443/"
    chef.validation_key_path = "chef-validator.pem"
    chef.node_name = "chef-vagrant0"
    #chef.run_list = ["recipe[nginx]", "role[frontend]"]
    chef.delete_node = true
    chef.delete_client = true
  end

end


