
Vagrant.configure("2") do |config|
  
  config.vm.box = "centos/7"

  config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  config.vm.provision "shell", path: "https://raw.githubusercontent.com/nbnodejs/vagrant-scripts/master/puppet_common.sh"

  config.vm.define "master" do |master|
    master.vm.hostname = "master"
    master.vm.network "private_network", ip: "192.168.10.10"
    master.vm.provision "file",
      source: "./puppet-master/files/puppet.conf.master",
      destination: "/vagrant/puppets.conf.master"
    master.vm.provision "file",
      source: "./puppet-master/hosts.master",
      destination: "/vagrant/hosts.master"
    master.vm.provision "shell", path: "https://raw.githubusercontent.com/nbnodejs/vagrant-scripts/master/puppet_master.sh"
  end


  config.vm.define "client" do |client|
    client.vm.hostname = "client"
    client.vm.network "private_network", ip: "192.168.10.11"
    client.vm.provision "file",
      source: "./puppet-client/files/puppet.conf.client",
      destination: "/vagrant/puppets.conf.client"
    client.vm.provision "file",
      source: "./puppet-client/hosts.client",
      destination: "/vagrant/hosts.client"
    client.vm.provision "shell", path: "https://raw.githubusercontent.com/nbnodejs/vagrant-scripts/master/puppet_client.sh"
  end

  config.vm.define "newnode" do |newnode|
    newnode.vm.hostname = "client"
    newnode.vm.network "private_network", ip: "192.168.10.12"
    newnode.vm.provision "file",
      source: "./puppet-client/files/puppet.conf.client",
      destination: "/vagrant/puppets.conf.client"
    newnode.vm.provision "file",
      source: "./puppet-client/hosts.client",
      destination: "/vagrant/hosts.client"
    newnode.vm.provision "shell", path: "https://raw.githubusercontent.com/nbnodejs/vagrant-scripts/master/puppet_client.sh"
  end

end
