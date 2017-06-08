# -*- mode: ruby -*-

Vagrant.configure("2") do |config|
  config.vm.define "web" do |web|
    web.vm.box = "bento/centos-7.2"
    #forwarding ports. If port 8080 is blocked by another process , Vagrant auto reassign it with auto_correct
    web.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true
    #create shared folder from working directory-vagrantsite to /opt/vagransite on guest
    #For using NFS share just add type:"nfs" to next string, or for SMB share use type:"smb"
    web.vm.synced_folder "vagrantsite/", "/opt/vagrantsite"
    #Provision section
    web.vm.provision "shell", inline: "yum install -y httpd"
    web.vm.provision "shell", inline: "service httpd start; ln -s /opt/vagrantsite /var/www/html"
    #configurate VM's options. For different providers options will be different
    web.vm.provider "virtualbox" do |vbox|
      vbox.memory = 1024
      vbox.cpus = 1
    end
  end  
end
