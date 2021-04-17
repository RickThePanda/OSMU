vagrant.configure("2") do |config|

  config.vm.define "client1" do |client1|
      client1.vm.network  "public_network", ip: "192.168.1.3"
      client1.vm.hostname = "client1"
      client1.vm.provider "virtualbox" do |vb|
         vb.memory = "4096"
      end
      client1.vm.provision "shell",
                    inline: "
                    ssh-keygen -b 4096 -t rsa -f ~/.ssh/genkey
                    ssh-copy-id vagrant@192.168.1.1

"

  end

  config.vm.define "client2" do |client2|
      client2.vm.network  "public_network", ip: "192.168.1.2"
      client2.vm.hostname = "client2"
      client2.vm.provider "virtualbox" do |vb|
         vb.memory = "4096"
      end
      client2.vm.provision "shell",
                    inline: "
                    ssh-keygen -b 4096 -t rsa -f ~/.ssh/genkey
                    ssh-copy-id vagrant@192.168.1.1"

  end

  config.vm.define "serverMachine" do |serverMachine|
      serverMachine.vm.network  "public_network", ip: "192.168.1.1"
      serverMachine.vm.hostname = "serverMachine"
      serverMachine.vm.provider "virtualbox" do |vb|
         vb.memory = "4096"
      end
      serverMachine.vm.provision "shell",
                    inline: "
                    ssh-keygen -b 4096 -t rsa -f ~/.ssh/genkey
                    ssh-copy-id vagrant@192.168.1.2
                    ssh-copy-id vagrant@192.168.1.3
                    ssh vagrant@192.168.1.2
                    sudo passwd -l root
                    scp vagrant@192.168.1.2:config.txt
                    chmod 777 config.txt
                    tar -cf archive.tar config.txt
                    sudo nano /etc/ssh/sshd_config
                    sudo systemctl restart ssh
                    "
      serverMachine.vm.provision "shell",
                    inline: "
                    ssh vagrant@192.168.1.3
                    sudo passwd -l root
                    scp vagrant@192.168.1.3:config.txt
                    chmod 777 config.txt
                    tar -cf archive.tar config.txt
                    sudo nano /etc/ssh/sshd_config
                    sudo systemctl restart ssh
                    "

  end

end