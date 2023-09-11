# -*- mode: ruby -*-
# vim: set ft=ruby :

Vagrant.configure(2) do |config| # WEB сервер 
    config.vm.define "Dynamicweb" do |vmconfig| 
         vmconfig.vm.box = 'bento/ubuntu-20.04'
         vmconfig.vm.hostname = 'DynamicWeb'
         vmconfig.vm.network "private_network", ip: "192.168.56.10"
         # форвардим порты развернутых сервисов на хост
         vmconfig.vm.network "forwarded_port", guest: 80, host: 80
         vmconfig.vm.network "forwarded_port", guest: 443, host: 443
         vmconfig.vm.network "forwarded_port", guest: 9100, host: 9100
         vmconfig.vm.provider "virtualbox" do |vbx|
          vbx.memory = "2048"
          vbx.cpus = "2"
          vbx.customize ["modifyvm", :id, '--audio', 'none']
         end
        end
    
    
    
        config.vm.define "Grafana" do |vmconfig| # сервер мониторинга, алертинга, централизованноого сбора логов
          vmconfig.vm.box = 'bento/ubuntu-20.04'
          vmconfig.vm.hostname = 'Monitoring'
          vmconfig.vm.network "private_network", ip: "192.168.56.20"
          # форвардим порты развернутых сервисов на хост
          vmconfig.vm.network "forwarded_port", guest: 9090, host: 9090
          vmconfig.vm.network "forwarded_port", guest: 3000, host: 3000
          vmconfig.vm.network "forwarded_port", guest: 8080, host: 8080
          vmconfig.vm.network "forwarded_port", guest: 9093, host: 9093
          vmconfig.vm.network "forwarded_port", guest: 514, host: 514
          vmconfig.vm.provider "virtualbox" do |vbx|
           vbx.memory = "2048"
           vbx.cpus = "2"
           vbx.customize ["modifyvm", :id, '--audio', 'none']
          end
         end
    
       config.vm.provision "ansible" do |ansible|
          ansible.playbook = "prov.yml"
          ansible.verbose = "v"
       end
     
end
