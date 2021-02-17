$lab_script = <<SCRIPT
cat <<EOF >> /etc/hosts
172.24.0.12 storage1.example.com storage1
172.24.0.13 storage2.example.com storage2
172.24.0.14 storage3.example.com storage3
EOF
SCRIPT

hosts = [

  { :hostname => "storage1.example.com",  :ip => "172.24.0.12", :cpu => "1", :ram => "2048" },

  { :hostname => "storage2.example.com",  :ip => "172.24.0.13", :cpu => "1", :ram => "2048" },

  { :hostname => "storage3.example.com",  :ip => "172.24.0.14", :cpu => "1", :ram => "2048" },

]

Vagrant.configure(2) do |config|
    config.ssh.insert_key = false
    config.ssh.forward_agent = true
    check_guest_additions = true
    functional_vboxsf = false
    config.vm.box = "centos/7"
    hosts.each do |host|

        config.vm.hostname = host[:hostname]
    
        config.vm.define host[:hostname] do |machine|
    
          machine.vm.network "private_network", ip: host[:ip]
    
          machine.vm.provider "virtualbox" do |v|
    
            v.name = host[:hostname]
    
            v.cpus = host[:cpu]
    
            v.memory = host[:ram]
    
          end
    
        end
    
      end
    
    end