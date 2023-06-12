Vagrant.configure("2") do |config|
    config.vm.box = "generic/ubuntu2004"
    config.vm.box_version = "3.6.8"
    config.vm.hostname = "morning-guest-vm"
    config.vm.network "private_network", ip: "192.168.56.20"

    config.vm.provider "virtualbox" do |vb|
        vb.name = "morning-guest-vm"
        vb.memory = 1024
        vb.cpus = 1
    end

    config.vm.provision "shell" do |s|
        ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
        s.inline = <<-SHELL
            # Create ci user
            useradd -s /bin/bash -d /home/ci/ -m -G sudo ci
            echo 'ci ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers
            mkdir -p /home/ci/.ssh && chown -R ci /home/ci/.ssh
            echo #{ssh_pub_key} >> /home/ci/.ssh/authorized_keys
        SHELL
    end
end