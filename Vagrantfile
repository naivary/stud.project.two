Vagrant.configure("2") do |config|
  config.vm.define "infra" do |infra|
    infra.vm.hostname = "k8s-infra-system"
    infra.vm.box = "ubuntu/focal64"
    infra.vm.boot_timeout = 300
    infra.vm.provider "virtualbox" do |v|
      v.name = "k8s-infra-system"
      v.memory = 4000
      v.cpus = 1
    end
    infra.vm.synced_folder ".", "/vagrant", disabled: true
    infra.vm.network "private_network", type: "", ip: "192.168.56.81"
    infra.vm.network "public_network", bridge: "enp0s25"
    infra.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/id_rsa.pub"
    infra.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update -y && sudo apt-get upgrade -y
    SHELL
  end

  config.vm.define "m1" do |m1|
    m1.vm.hostname = "k8s-m1"
    m1.vm.box = "ubuntu/focal64"
    m1.vm.boot_timeout = 300
    m1.vm.provider "virtualbox" do |v|
      v.name = "m1"
      v.memory = 4000
      v.cpus = 1
    end
    m1.vm.synced_folder ".", "/vagrant", disabled: true
    m1.vm.network "private_network", type: "", ip: "192.168.56.61"
    m1.vm.network "public_network", bridge: "enp0s25"
    m1.vm.disk :disk, size:"30GB", primary: true
    m1.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/id_rsa.pub"
    m1.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update -y && sudo apt-get upgrade -y
      cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
    SHELL
  end

  config.vm.define "m2" do |m2|
    m2.vm.hostname = "k8s-m2"
    m2.vm.box = "ubuntu/focal64"
    m2.vm.boot_timeout = 300
    m2.vm.provider "virtualbox" do |v|
      v.name = "m2"
      v.memory = 4000
      v.cpus = 1
    end
    m2.vm.synced_folder ".", "/vagrant", disabled: true
    m2.vm.network "private_network", type: "", ip: "192.168.56.62"
    m2.vm.network "public_network", bridge: "enp0s25"
    m2.vm.disk :disk, size:"30GB", primary: true
    m2.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/id_rsa.pub"
    m2.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update -y && sudo apt-get upgrade -y
      cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
    SHELL
  end

  config.vm.define "m3" do |m3|
    m3.vm.hostname = "k8s-m3"
    m3.vm.box = "ubuntu/focal64"
    m3.vm.boot_timeout = 300
    m3.vm.provider "virtualbox" do |v|
      v.name = "m3"
      v.memory = 4000
      v.cpus = 1
    end
    m3.vm.synced_folder ".", "/vagrant", disabled: true
    m3.vm.network "private_network", type: "", ip: "192.168.56.63"
    m3.vm.network "public_network", bridge: "enp0s25"
    m3.vm.disk :disk, size:"30GB", primary: true
    m3.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/id_rsa.pub"
    m3.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update -y && sudo apt-get upgrade -y
      cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
    SHELL
  end

  config.vm.define "n1" do |n1|
    n1.vm.hostname = "k8s-n1"
    n1.vm.box = "ubuntu/focal64"
    n1.vm.boot_timeout = 300
    n1.vm.provider "virtualbox" do |v|
      v.name = "n1"
      v.memory = 2000
      v.cpus = 1
    end
    n1.vm.synced_folder ".", "/vagrant", disabled: true
    n1.vm.network "private_network", type: "", ip: "192.168.56.51"
    n1.vm.network "public_network", bridge: "enp0s25"
    n1.vm.disk :disk, size:"30GB", primary: true
    n1.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/id_rsa.pub"
    n1.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update -y && sudo apt-get upgrade -y
      cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
    SHELL
  end

  config.vm.define "n2" do |n2|
    n2.vm.hostname = "k8s-n2"
    n2.vm.box = "ubuntu/focal64"
    n2.vm.boot_timeout = 300
    n2.vm.provider "virtualbox" do |v|
      v.name = "n2"
      v.memory = 2000
      v.cpus = 1
    end
    n2.vm.synced_folder ".", "/vagrant", disabled: true
    n2.vm.network "private_network", type: "", ip: "192.168.56.52"
    n2.vm.network "public_network", bridge: "enp0s25"
    n2.vm.disk :disk, size:"30GB", primary: true
    n2.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/id_rsa.pub"
    n2.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update -y && sudo apt-get upgrade -y
      cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
    SHELL
  end
  
end
