Vagrant.configure("2") do |config|

    config.vm.box = "ubuntu/trusty64" 
    # config.vm.box = "debian/contrib-buster64"

    config.vm.network "forwarded_port", guest: 80, host: 8080
    # config.vm.network "private_network", ip: "192.165.33.10"
    config.vm.network "private_network", ip: "192.168.56.1"      
 
    config.ssh.username = 'vagrant'
    config.ssh.password = 'vagrant'
    config.ssh.keys_only = false

    config.vm.define "trusty" do |node|    
      node.vm.hostname = "trusty.local"    
        node.vm.provision "ansible" do |ansible|        
          ansible.playbook = "main.yml"
      end
    end

    config.vm.provider "virtualbox" do |vb|
        vb.memory = "512"
        vb.cpus = "1"
    end
 
   config.vm.provision "shell", inline: <<-SHELL 
        apt-get update                          
        sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config    
        # systemctl restart sshd.service  ## not found
        sudo /etc/init.d/ssh restart      ## fixed trying @CLI
       SHELL
    end

