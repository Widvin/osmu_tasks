
Vagrant.configure("2") do |config|

  
  
 # config.vm.provision "shell", inline: "echo Hello"
  
 # config.vm.define "vm1" do |vm1|
 # vm1.vm.box = "ubuntu/hirsute64"
 # vm1.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
 # vm1.vm.synced_folder "c:/Users/XXX/d/projects", "/var/www"
 # end

 # config.vm.define "vm2" do |vm2|
 # vm2.vm.box = "ubuntu/hirsute64"
 # vm2.vm.network "forwarded_port", guest: 81, host: 8081, host_ip: "127.0.0.2"
 # vm2.vm.synced_folder "c:/Users/XXX/d/projects", "/var/www2"
 # end
  
  
  servers=[
	{
	:hostname => "vm1",
	:box => "ubuntu/xenia164",
	:ip => "172.16.1.22",
	:ssh_port => '2202'
	},
		{
	:hostname => "vm2",
	:box => "ubuntu/xenia64",
	:ip => "172.16.1.23",
	:ssh_port => '2203'
	}
  ]
  
  
  servers.each do |machine|
		config.vm.define machine[:hostname] do |node|
			node.vm.box = machine[:box]
			node.vm.hostname = machine[:hostname]
			node.vm.network :private_network, ip: machine[:ip]
			node.vm.network "forwarded_port", guest: 22, host: machine[:ssh_port], id: "ssh"
			node.vm.synced_folder "c:/Users/XXX/d/projects", "/var/www"
			
			node.vm.provision "shell", 
			inline: "
			sudo apt-get update
			sudo apt-get install git
			git init .
			git remote add -f origin  https://github.com/Widvin/osmu_tasks
			git checkout Tusk2
			git show :tusk2.txt
			git remote
			",
			run: "always",
			privileged: "false"
			
			 
			node.vm.provider :virtualbox do |vb|
				vb.customize ["modifyvm", :id, "--memory", 1024]
				vb.customize ["modifyvm", :id, "--cpus", 2]
			end
				
		end
	
	end
	
end
