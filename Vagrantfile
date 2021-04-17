$script = <<-'SCRIPT'
sudo apt-get update && upgrade
sudo apt-get install git -y
git clone -b lab2 https://github.com/RickThePanda/OSMU
cat ~/osmu/file.txt
SCRIPT

Vagrant.configure("2") do |config|
        config.vm.define "Ubuntu1" do |conf|
          conf.vm.box = "ubuntu/trusty64"
          conf.vm.hostname = "Starik_Ubunty1"
          conf.vm.network :private_network, ip: "192.168.10.16"

          conf.vm.provider :virtualbox do |vb|
              vb.customize [
                  "modifyvm", :id,
                  "--memory", "1024",
                  "--cpus", "1"
              ]
          end

          conf.vm.provision "shell", inline: $script
end

        config.vm.define "Ubuntu2" do |conf|
          conf.vm.box = "ubuntu/trusty64"
          conf.vm.hostname = "Starik_Ubunty2"
          conf.vm.network :private_network, ip: "192.168.10.17"

          conf.vm.provider :virtualbox do |vb|
              vb.customize [
                  "modifyvm", :id,
                  "--memory", "1024",
                  "--cpus", "1"
              ]
          end

          conf.vm.provision "shell", inline: $script
      end
  end