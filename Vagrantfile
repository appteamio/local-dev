# -*- mode: ruby -*-
# vi: set ft=ruby :
VAGRANTFILE_API_VERSION = '2'
Vagrant.require_version '>= 1.5.0'
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.hostname = 'local-dev'
  config.omnibus.chef_version = 'latest'
  config.vm.box = 'ubuntu/trusty64'
  config.vm.network :private_network, type: 'dhcp'
  config.vm.synced_folder "../data", "/apps"
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = [:host, "cookbooks"]
    chef.provisioning_path = "/vagrant-chef"
    chef.json = {
      user: {
                  name: "vagrant",
                  "password": "#Shadow_hashed_password_here" #use command: openssl passwd -1 "theplaintextpassword"
                },
      git:{
                  name: "jalil",
                  email: "jalil@appteam.io" 
                  },
      db: {
              root_password: "pass_here",
              user: {
                name: "jalil",
                password: "pass_here"
              }
            }
    }
    chef.run_list = [
      'recipe[crockpot::default]',
      'recipe[crockpot::nodejs]',
      'recipe[crockpot::postgres]',
      'recipe[crockpot::rbenv]',
      'recipe[crockpot::gitconf]',
      'recipe[crockpot::sshconf]'
    ]
  end
end
