VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.ssh.insert_key = false
  config.ssh.forward_agent = true

  config.vm.provision :hosts do |provisioner|

      provisioner.add_host '192.168.56.101', ['client']
      provisioner.add_host '192.168.56.102', ['server']

  end

  config.vm.define "client" do |client|
    client.vm.box = 'ubuntu/bionic64'
    client.vm.hostname = 'client'

    client.vm.network :private_network, ip: "192.168.56.101"
    client.vm.network :forwarded_port, guest: 22, host: 10122, id: "ssh"

    client.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "client"]
    end
  end

  config.vm.define "server" do |server|
    server.vm.box = 'ubuntu/bionic64'
    server.vm.hostname = 'server'

    server.vm.network :private_network, ip: "192.168.56.102"
    server.vm.network :forwarded_port, guest: 22, host: 10222, id: "ssh"

    server.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "server"]
    end
  end


  config.vm.provision :shell, path: "bootstrap.sh"

end