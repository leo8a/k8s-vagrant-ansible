# -*- mode: ruby -*-
# vi:set ft=ruby sw=2 ts=2 sts=2:


# Define the number of worker nodes
NUM_WORKER_NODE = 2
IMAGE_NAME = "ubuntu/bionic64"


Vagrant.configure("2") do |config|
  config.ssh.insert_key = false
  config.vm.box_check_update = false

  config.vm.provider "virtualbox" do |v|
    v.memory = 4096
    v.cpus = 2
  end

  config.vm.define "kubemaster" do |master|
    master.vm.box = IMAGE_NAME
    master.vm.hostname = "k8s-master"
    master.vm.network "private_network", ip: "192.168.50.10"

    master.vm.provision "ansible" do |ansible|
      ansible.playbook = "kubernetes-setup/master-playbook.yml"
      ansible.extra_vars = { node_ip: "192.168.50.10", }
    end
  end

  (1..NUM_WORKER_NODE).each do |i|
    config.vm.define "kubenode0#{i}" do |node|

      node.vm.box = IMAGE_NAME
      node.vm.hostname = "node-#{i}"
      node.vm.network "private_network", ip: "192.168.50.#{i + 10}"

      node.vm.provision "ansible" do |ansible|
        ansible.playbook = "kubernetes-setup/node-playbook.yml"
        ansible.extra_vars = { node_ip: "192.168.50.#{i + 10}", }
      end
    end
  end

end
