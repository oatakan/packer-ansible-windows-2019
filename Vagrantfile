# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  win_hostname= "win2019"

  config.vm.define "#{win_hostname}" do |node|
    node.vm.box = "file://builds/windows-2019-virtualbox.box"
    node.vm.hostname = "#{win_hostname}"
    node.vm.boot_timeout = 600
    node.winrm.transport = :negotiate
    node.vm.communicator = "winrm"
    node.winrm.basic_auth_only = false
    node.winrm.timeout = 300
    node.winrm.retry_limit = 20
    node.vm.network "forwarded_port", guest: 5986, host: 5986
    node.vm.network :private_network, ip: "10.0.1.4", gateway: "10.0.1.1"

    node.vm.provider "virtualbox" do |vb, override|
      vb.gui = false
      vb.name = "#{win_hostname}"
      vb.default_nic_type = "82545EM"
      vb.customize ["modifyvm", :id, "--memory", 4096]
      vb.customize ["modifyvm", :id, "--cpus", 2]
      vb.customize ["modifyvm", :id, "--vram", "32"]
      vb.customize ["setextradata", "global", "GUI/SuppressMessages", "all" ]
    end
  end
end