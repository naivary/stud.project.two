Vagrant.configure("2") do |config|
  config.vm.define "mn1" do |mn1|
    mn1.vm.hostname = "mn1"
    mn1.vm.box = "ubuntu/focal64"
    mn1.vm.boot_timeout = 300
    mn1.vm.provider "virtualbox" do |v|
      v.name = "mn1"
      v.memory = 4000
      v.cpus = 1
    end
    mn1.vm.synced_folder ".", "/vagrant", disabled: true
    mn1.vm.network "private_network", type: "", ip: "192.168.56.80"
    mn1.vm.network "public_network", bridge: "enp0s25"
    mn1.vm.disk :disk, size:"30GB", primary: true
    mn1.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/id_rsa.pub"
    mn1.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update -y && sudo apt-get upgrade -y
      cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
    SHELL
  end

  config.vm.define "mn2" do |mn2|
    mn2.vm.hostname = "mn2"
    mn2.vm.box = "ubuntu/focal64"
    mn2.vm.boot_timeout = 300
    mn2.vm.provider "virtualbox" do |v|
      v.name = "mn2"
      v.memory = 4000
      v.cpus = 1
    end
    mn2.vm.synced_folder ".", "/vagrant", disabled: true
    mn2.vm.network "private_network", type: "", ip: "192.168.56.81"
    mn2.vm.network "public_network", bridge: "enp0s25"
    mn2.vm.disk :disk, size:"30GB", primary: true
    mn2.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/id_rsa.pub"
    mn2.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update -y && sudo apt-get upgrade -y
      cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
    SHELL
  end

  config.vm.define "mn3" do |mn3|
    mn3.vm.hostname = "mn3"
    mn3.vm.box = "ubuntu/focal64"
    mn3.vm.boot_timeout = 300
    mn3.vm.provider "virtualbox" do |v|
      v.name = "mn3"
      v.memory = 4000
      v.cpus = 1
    end
    mn3.vm.synced_folder ".", "/vagrant", disabled: true
    mn3.vm.network "private_network", type: "", ip: "192.168.56.82"
    mn3.vm.network "public_network", bridge: "enp0s25"
    mn3.vm.disk :disk, size:"30GB", primary: true
    mn3.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/id_rsa.pub"
    mn3.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update -y && sudo apt-get upgrade -y
      cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
    SHELL
  end

  config.vm.define "wn1" do |wn1|
    wn1.vm.hostname = "wn1"
    wn1.vm.box = "ubuntu/focal64"
    wn1.vm.boot_timeout = 300
    wn1.vm.provider "virtualbox" do |v|
      v.name = "wn1"
      v.memory = 2000
      v.cpus = 1
    end
    wn1.vm.synced_folder ".", "/vagrant", disabled: true
    wn1.vm.network "private_network", type: "", ip: "192.168.56.90"
    wn1.vm.network "public_network", bridge: "enp0s25"
    wn1.vm.disk :disk, size:"30GB", primary: true
    wn1.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/id_rsa.pub"
    wn1.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update -y && sudo apt-get upgrade -y
      cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
    SHELL
  end

  config.vm.define "wn2" do |wn2|
    wn2.vm.hostname = "wn2"
    wn2.vm.box = "ubuntu/focal64"
    wn2.vm.boot_timeout = 300
    wn2.vm.provider "virtualbox" do |v|
      v.name = "wn2"
      v.memory = 2000
      v.cpus = 1
    end
    wn2.vm.synced_folder ".", "/vagrant", disabled: true
    wn2.vm.network "private_network", type: "", ip: "192.168.56.91"
    wn2.vm.network "public_network", bridge: "enp0s25"
    wn2.vm.disk :disk, size:"30GB", primary: true
    wn2.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/id_rsa.pub"
    wn2.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update -y && sudo apt-get upgrade -y
      cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
    SHELL
  end
  
end
