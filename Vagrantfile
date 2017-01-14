required_plugins = %w(vagrant-host-shell vagrant-docker-compose)
required_plugins.each do |plugin|
  system "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

Vagrant.configure("2") do |config|
  config.vm.define :ubuntu do |ubuntu|
    
    ubuntu.vm.hostname = :ubuntu
    ubuntu.vm.box = 'parallels/ubuntu-14.04'

    ubuntu.vm.provider :parallels do |prl|
      prl.cpus = 2
      prl.memory = 1024 # works with 1024, 512 will need a swap file
    end

    port = 4200

    config.vm.network "private_network", ip: "192.168.0.2"
    config.vm.network "forwarded_port", guest: port, host: port
    config.vm.provision :docker
    config.vm.provision :docker_compose, yml:'/vagrant/docker-compose.yml', compose_version: "1.8.0"

  end

end