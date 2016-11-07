# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
  end

  config.vm.define :master do |master_config|
    master_config.vm.box = "ubuntu/trusty64"
    master_config.vm.host_name = 'saltmaster.local'
    master_config.vm.network "private_network", ip: "192.168.50.10"
    master_config.vm.synced_folder "../salt-formula/pillars/", "/srv/pillars"
    master_config.vm.synced_folder "../salt-formula/states/", "/srv/states"
    master_config.vm.synced_folder "../salt-deliveries/", "/srv/saltd"

    master_config.vm.provision :salt do |salt|
      salt.master_config = "saltstack/etc/master"
      salt.install_type = "stable"
      salt.install_master = true
      salt.no_minion = true
      salt.verbose = true
      salt.colorize = true
    end
  end

  config.vm.define :minion1 do |minion_config|
    minion_config.vm.box = "ubuntu/trusty64"
    minion_config.vm.host_name = 'saltminion1.local'
    minion_config.vm.network "private_network", ip: "192.168.50.11"
    minion_config.vm.synced_folder "saltstack/env/int1/grains", "/etc/salt/minion.d"

    minion_config.vm.provision :salt do |salt|
      salt.minion_config = "saltstack/env/int1/minion"
      salt.install_type = "stable"
      salt.verbose = true
      salt.colorize = true
    end
  end

  # config.vm.define :minion2 do |minion_config|
  #   minion_config.vm.box = "ubuntu/trusty64"
  #   minion_config.vm.host_name = 'saltminion2.local'
  #   minion_config.vm.network "private_network", ip: "192.168.50.12"
  #   minion_config.vm.synced_folder "saltstack/env/int2/grains", "/etc/salt/minion.d"

  #   minion_config.vm.provision :salt do |salt|
  #     salt.minion_config = "saltstack/env/int2/minion"
  #     salt.install_type = "stable"
  #     salt.verbose = true
  #     salt.colorize = true
  #   end
  # end

end
