Vagrant.configure("2") do |config|
  # Configuration de la machine ansible
  config.vm.define "ansible" do |ansible_config|
    ansible_config.vm.box = "bento/ubuntu-20.04"
    ansible_config.vm.hostname = "ansible"
    ansible_config.vm.network "private_network", type: "static", ip: "192.168.99.20"

    ansible_config.vm.provider "vmware_desktop" do |v|
      v.memory = 2048
      v.cpus = 2
    end

    ansible_config.vm.provision :shell, inline: <<-SHELL
      apt update
      apt install -y ansible
    SHELL
  end

  # Configuration des clients
  (1..2).each do |i|
    config.vm.define "client#{i}" do |client|
      client.vm.box = "bento/ubuntu-20.04"
      client.vm.hostname = "client#{i}"
      client.vm.network "private_network", type: "static", ip: "192.168.99.2#{i}"

      client.vm.provider "vmware_desktop" do |v|
        v.memory = 1024
        v.cpus = 1
      end

      client.vm.provision :shell, inline: <<-SHELL
        apt update
        apt install -y openssh-server
      SHELL
    end
  end
end
