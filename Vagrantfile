# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure(2) do |config|

    config.vm.box = "bento/centos-7.2"

    config.vm.define "controller" do |cn|

        cn.vm.hostname="controller"

        cn.vm.network "forwarded_port", guest: 80,      host: 8080
        cn.vm.network "forwarded_port", guest: 6080,      host: 6080

        cn.vm.provider "virtualbox" do |vb|
            vb.memory = "4096"
        end

        cn.vm.provision "shell" do |shell|
            shell.inline = "sudo yum install -y centos-release-openstack-mitaka"
        end
        cn.vm.provision "shell" do |shell|
            shell.inline = "sudo yum update -y"
        end
        cn.vm.provision "shell" do |shell|
            shell.inline = "sudo yum install -y openstack-packstack"
        end
        # cn.vm.provision "shell" do |shell|
        #     shell.inline = "packstack --allinone"
        # end
        cn.vm.provision "shell" do |shell|
            shell.inline = "packstack --allinone --provision-demo=n --os-neutron-ovs-bridge-mappings=extnet:br-ex --os-neutron-ovs-bridge-interfaces=br-ex:eth0 --os-neutron-ml2-type-drivers=vxlan,flat"
        end

    end
end
