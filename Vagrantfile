Vagrant.configure("2") do |config|    
    config.vm.box = "ubuntu/bionic64"

    config.vm.provider "virtualbox" do |vb|
        vb.memory = 512
        vb.cpus = 1
    end

    config.vm.define "ansible_2" do |ansible|

        ansible.vm.network "private_network", ip: "172.17.177.2"

        ansible.vm.provision "shell", inline: "cp /vagrant/config/.ssh/id_bionic /home/vagrant && chmod 600 /home/vagrant/id_bionic && chown vagrant:vagrant /home/vagrant/id_bionic"
        ansible.vm.provision "shell", inline: "cat /vagrant/config/.ssh/id_bionic.pub >> .ssh/authorized_keys"

        ansible.vm.provision "shell",
            inline: "apt-get update && \
                     apt-get install -y software-properties-common && \
                     apt-add-repository --yes --update ppa:ansible/ansible && \
                     apt-get install -y ansible"        
    end

    config.vm.define "wordpress" do |wordpress|

        wordpress.vm.network "private_network", ip: "172.17.177.40"

        wordpress.vm.provision "shell", inline: "cat /vagrant/config/.ssh/id_bionic.pub >> .ssh/authorized_keys"
    end

    config.vm.define "mysql" do |mysql|
    
        mysql.vm.network "private_network", ip: "172.17.177.42"

        mysql.vm.provision "shell", inline: "cat /vagrant/config/.ssh/id_bionic.pub >> .ssh/authorized_keys"
    end
end