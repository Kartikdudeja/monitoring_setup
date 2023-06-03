# Zabbix & Grafana Monitoring System Test Lab

servers = [
    {
        # Database Node
        :hostname => "mon-db",
        :ip => "192.168.20.11",
        :memory => "1024",
        :cpu => "1",
        :vmname => "mon-db"
    },
    {
        # Production Node
        :hostname => "mon-prod",
        :ip => "192.168.20.12",
        :memory => "1024",
        :cpu => "1",
        :vmname => "mon-prod"
    },
    {
        # DR Node
        :hostname => "mon-dr",
        :ip => "192.168.20.13",
        :memory => "1024",
        :cpu => "1",
        :vmname => "mon-dr"
    },
    {
        # host Node
        :hostname => "mon-host",
        :ip => "192.168.20.14",
        :memory => "1024",
        :cpu => "1",
        :vmname => "mon-host"
    }
]

Vagrant.configure("2") do |config|

    # manages the /etc/hosts file on guest machines in multi-machine environments
    config.hostmanager.enabled = true
    config.hostmanager.manage_host = true

    servers.each do |machine|
    
        config.vm.define machine[:hostname] do |node|

            node.vm.box = "geerlingguy/centos7"
            node.vm.hostname = machine[:hostname]
            node.vm.network :private_network, ip: machine[:ip] #,
                # fix for device not reachable in internal network
                # virtualbox__intnet: true
 
            node.vm.network "public_network"

            node.vm.provider :virtualbox do |vb|

                vb.customize ["modifyvm", :id, "--name", machine[:vmname]]
                vb.customize ["modifyvm", :id, "--memory", machine[:memory]]
                vb.customize ["modifyvm", :id, "--cpus", machine[:cpu]]

                # fix for slow network speed issue
                vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
                vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]

            end # end provider
        end # end config
    end # end servers each loop
end
