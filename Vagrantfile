# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |dockersrv|

  dockersrv.vm.box = "/builds/box/centos7.4-template_virtualbox.box"
  dockersrv.vm.hostname = "dockersrv"
  dockersrv.vm.box_check_update = false
  dockersrv.vm.network "forwarded_port", guest: 8084, host: 8084

  dockersrv.ssh.username = "provisioner"
  dockersrv.ssh.private_key_path = "/builds/ssh_keys/provisioner.priv"
  dockersrv.vm.synced_folder ".", "/vagrant", disabled: true

  dockersrv.vm.provider "virtualbox" do |vb|
     vb.gui = false
     vb.cpus = 1
     vb.memory = "1024"
  end
  
  # Install Docker-CE
  dockersrv.vm.provision "ansible" do |dockerinstall|
    dockerinstall..force_remote_user = "provisioner"
    dockerinstall.playbook = "install_dockerce.yml"
  end

  # Install Node App 
  dockersrv.vm.provision "ansible" do |nodeinstall|
    nodeinstall.force_remote_user = "provisioner"
    nodeinstall.playbook = "install_nodeapp.yml"
  end

end
