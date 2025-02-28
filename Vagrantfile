# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"
  config.vm.network "private_network", ip: "192.168.100.100"
  
  config.vm.provider "virtualbox" do |vb|
    vb.cpus = 2
    vb.memory = 4096
  end

  install_deps = <<-SHELL
    sudo apt update
    sudo apt install -y openjdk-17-jdk
  SHELL

  config.vm.provision "shell", inline: install_deps
  
  config.trigger.after :up do |trigger|
    trigger.info = "Starting the Java application..."
    trigger.run = {
      inline: "cd /vagrant && ./gradlew bootRun"
    }
  end
end
