ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure(2) do |config|

    config.vm.provision "shell", path: "bootstrap.sh"

    #kubernetes Master Server
    config.vm.define "master" do |master|
        master.vm.box = "centos/7"
        master.vm.hostname = "master.mercure.form"
        master.vm.network "private_network", ip: "172.42.42.100"
        master.vm.provider "virtualbox" do |v|
            v.name = "master"
            v.memory = 2048
            v.cpus = 2
            #Prevent virtualbox from interfering with host audio stack
            v.customize ["modifyvm", :id, "--audio", "none"]
        end
        #master.vm.provision "shell", path: "bootstrap_master.sh"
    end
    NodeCount = 3

    #kubernetes Worker Nodes
    (1..NodeCount).each do |i|
        config.vm.define "worker#{i}" do |workernode|
            workernode.vm.box = "centos/7"
            workernode.vm.hostname = "worker#{i}.mercure.form"
            workernode.vm.network "private_network", ip: "172.42.42.10#{i}"
            workernode.vm.provider "virtualbox" do |v|
                v.name = "worker#{i}"
                v.memory = 1024
                v.cpus = 1
                #Prevent VirtualBox from interfering with host audio stack
                v.customize ["modifyvm", :id, "--audio", "none"]
            end
        #workernode.vm.provision "shell", path: "bootstrap_worker.sh"
        end
    end
end
        