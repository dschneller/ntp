# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.

  config.vm.box = "ubuntu/trusty64"

  # config.vm.box_check_update = false

 # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  (1..2).each do |i|
      config.vm.define "ntptest-#{i}" do |node|
        port1 = (i + 7) * 1000 + 80
        port2 = (i + 7) * 1000 + 404
        octet = i + 10
        node.vm.hostname = "ntptest-#{i}"
        node.vm.network "private_network", ip: "192.168.33.#{octet}"
        node.vm.provision "shell" do |s|
          s.args = [ i ]
          s.inline = <<-SHELL
            sudo locale-gen de_DE.UTF-8
            sudo apt-get update
            sudo cp /vagrant/ntp.${1}.conf /etc/ntp.conf
            sudo chown root:root /etc/ntp.conf
            sudo chmod 0644 /etc/ntp.conf
            sudo apt-get -o Dpkg::Options::="--force-confold" --force-yes -y install ntp
          SHELL
        end
      end
   end
end
