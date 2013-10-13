Vagrant.configure("2") do |config|
  config.vm.box = "precise64"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

 config.vm.synced_folder "srv", "/srv/"
 config.vm.provision :salt do |salt|
    salt.minion_config = "srv/minion"
    salt.run_highstate = true
 end

  config.vm.define "web" do |web|
    web.vm.network :forwarded_port, guest: 80, host: 8080
    web.vm.network :private_network, ip: "192.168.56.101"
    web.vm.synced_folder "/Users/binish.ar/dev", "/home/vagrant/dev", :extra => "dmode=755,fmode=644"
    web.vm.hostname = "web"
  end

 config.vm.synced_folder "/Users/binish.ar/dev", "/home/vagrant/dev", :extra => "dmode=555,fmode=644"

  config.vm.define "admin" do |admin|
    admin.vm.network :private_network, ip: "192.168.56.102"
    admin.vm.hostname = "admin"
  end

  config.vm.box = "lucid64"

  config.vm.define "hadoop" do |hadoop|
    hadoop.vm.network :private_network, ip: "192.168.56.103"
    hadoop.vm.hostname = "hadoop"
  end


  config.vm.define "grid" do |grid|
    grid.vm.network :private_network, ip: "192.168.56.104"
    grid.vm.hostname = "grid"
  end

end
