Vagrant.configure("2") do |config|
    config.vm.provider :virtualbox do |v|
        config.vm.box = "precise64"
        config.vm.box_url = "http://files.vagrantup.com/precise64.box"

        v.name = "Spring Web"
        v.customize ["modifyvm", :id, "--memory", 512]
        config.vm.network :private_network, ip: "10.10.10.10"
    end

    config.ssh.forward_agent = true

    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/provision.yml"
        ansible.extra_vars = {
            databases: ['testing']
        }
    end

    config.vm.synced_folder "./", "/vagrant", id: "vagrant-root", :nfs => true
end
