Vagrant.configure("2") do |config|
  
  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 2
  end

  config.vm.box = "hashicorp/bionic64"
  
  config.vm.hostname = "dockerbox"
  
  config.vm.network "forwarded_port", guest: 2200, host: 2200,
    auto_correct: true
  config.vm.usable_port_range = 2000..2999
  
  config.vm.network "forwarded_port", guest: 3389, host: 3399,
    auto_correct: true
  config.vm.usable_port_range = 3389..3400
  
  config.vm.provision "update",
    type: "shell",
    preserve_order: true,
    inline: "apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y -o Dpkg::Options::='--force-confdef' -o Dpkg::Options::='--force-confold' upgrade"
  
  config.vm.provision "docker"
  
  config.vm.provision "add to sudo",
    type: "shell",
    preserve_order: true,
    inline: "usermod -aG docker $USER"
    
  config.vm.provision "docker-compose",
    type: "shell",
    preserve_order: true,
    inline: "sudo apt-get install -y docker-compose && sudo apt-get install -y docker-compose --fix-missing"
    
  config.vm.provision "file", source: "./docker-compose.yml", destination: "~/xrdp/docker-compose.yml"
    
end
