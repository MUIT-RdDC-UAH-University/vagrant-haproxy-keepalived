# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/xenial32"
# config.vm.box_url = "http://files.vagrantup.com/precise32.box"
  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", 256]
    v.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
  end

  config.vm.define :haproxy1, primary: true do |haproxy1_config|
    haproxy1_config.vm.hostname = 'haproxy1'  
    haproxy1_config.vm.network :private_network, ip: "192.168.2.9"
    haproxy1_config.ssh.forward_agent = true
    haproxy1_config.ssh.forward_x11 = true
    haproxy1_config.vm.provision "shell" do |s|
      s.path = "haproxy-setup.sh"
      s.args = "101"
    end
    haproxy1_config.vm.provider :virtualbox do |vb|
        vb.customize ['modifyvm', :id, '--nictrace2', 'on']
        vb.customize ['modifyvm', :id, '--nictracefile2', 'haproxy1_trace2.pcap']
    end
  end

  config.vm.define :haproxy2, primary: true do |haproxy2_config|
    haproxy2_config.vm.hostname = 'haproxy2'
    haproxy2_config.vm.network :private_network, ip: "192.168.2.10"
    haproxy2_config.ssh.forward_agent = true
    haproxy2_config.ssh.forward_x11 = true
    haproxy2_config.vm.provision "shell" do |s|
      s.path = "haproxy-setup.sh"
      s.args = "100"
    end
    haproxy2_config.vm.provider :virtualbox do |vb|
        vb.customize ['modifyvm', :id, '--nictrace2', 'on']
        vb.customize ['modifyvm', :id, '--nictracefile2', 'haproxy2_trace2.pcap']
    end
  end

  config.vm.define :web1 do |web1_config|
    web1_config.vm.hostname = 'web1'
    web1_config.vm.network :private_network, ip: "192.168.2.11"
    web1_config.vm.provision :shell, :path => "web-setup.sh"
    web1_config.vm.provider :virtualbox do |vb|
        vb.customize ['modifyvm', :id, '--nictrace2', 'on']
        vb.customize ['modifyvm', :id, '--nictracefile2', 'web1_trace2.pcap']
    end
  end

  config.vm.define :web2 do |web2_config|
    web2_config.vm.hostname = 'web2'
    web2_config.vm.network :private_network, ip: "192.168.2.12"
    web2_config.vm.provision :shell, :path => "web-setup.sh"
    web2_config.vm.provider :virtualbox do |vb|
        vb.customize ['modifyvm', :id, '--nictrace2', 'on']
        vb.customize ['modifyvm', :id, '--nictracefile2', 'web2_trace2.pcap']
    end
  end
end

