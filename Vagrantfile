IMAGE_NAME = ENV["IMAGE_NAME"] || "bento/ubuntu-21.04"
MASTER_MEMORY = ENV["MASTER_CPUS"] || 4096
MASTER_CPUS = ENV["MASTER_CPUS"] || 2
WORKER_NODES = ENV["WORKER_NODES"] || 2
WORKER_MEMORY = ENV["WORKER_MEMORY"] || 2048
WORKER_CPUS = ENV["WORKER_CPUS"] || 2
BASE_IP = ENV["BASE_IP"] || "10.50.0"

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false

  config.vm.define "k8s-master" do |master|
      master.vm.provider "virtualbox" do |v|
        v.memory = MASTER_MEMORY
        v.cpus = MASTER_CPUS
      end
      master.vm.box = IMAGE_NAME
      master.vm.network "private_network", ip: "#{BASE_IP}.#{10}"
      master.vm.hostname = "k8s-master"
  end

  (1..WORKER_NODES).each do |i|
      config.vm.define "node-#{i}" do |node|
          node.vm.provider "virtualbox" do |v|
            v.memory = WORKER_MEMORY
            v.cpus = WORKER_CPUS
          end
          node.vm.box = IMAGE_NAME
          node.vm.network "private_network", ip: "#{BASE_IP}.#{i + 10}"
          node.vm.hostname = "node-#{i}"
      end
  end
end