servers=[
   {
    :hostname => "local-markitplace",
    :ip => "192.168.13.10",
  },
]
Vagrant.configure(2) do |config|
    servers.each do |machine|
        config.vm.define machine[:hostname] do |node|
            node.vm.box = "centos/6"
            node.vm.hostname = machine[:hostname]
            node.vm.network "private_network", ip: machine[:ip]
            node.vm.provider "virtualbox" do |vb|
                vb.customize ["modifyvm", :id, "--memory", 4096]
                vb.customize ["modifyvm", :id, "--cpus", 2]
        end
        node.vm.provision "shell", path: "pre.sh"
	node.vm.provision "ansible" do |ansible|
	#	ansible.galaxy_role_file = "requirements.yml"
    		ansible.playbook = "ces_markitplace.yml"
  	end
    end
    end
end
