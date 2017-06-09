# -*- mode: ruby -*-

Vagrant.configure("2") do |config|


  config.vm.define "web" do |web|
    web.vm.box = "bento/centos-7.2"
    web.vm.hostname = "centos"
    #configurate network private . Instead ip we could use type: "dhcp"
    web.vm.network "private_network", ip: "192.168.100.2"
    #configuration public network bridged to interface
    web.vm.network "public_network", bridge: "Ethernet Connection I219-LM"
    #forwarding ports. If port 8080 is blocked by another process , Vagrant auto reassign it with auto_correct
    web.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true
    #create shared folder from working directory-vagrantsite to /opt/vagransite on guest
    #For using NFS share just add type:"nfs" to next string, or for SMB share use type:"smb"
    web.vm.synced_folder "vagrantsite/", "/opt/vagrantsite"
    #Provision section
    web.vm.provision "shell", inline: "yum install -y httpd"
    web.vm.provision "shell", inline: "service httpd start; ln -s /opt/vagrantsite /var/www/html"
    web.vm.provision "shell", path: "script.sh"
    #configurate VM's options. For different providers options will be different
    web.vm.provider "virtualbox" do |vbox|
      vbox.name = "new_vm"
      vbox.memory = 1024
      vbox.cpus = 1
    end
  end
  
    
end
