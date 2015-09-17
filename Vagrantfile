# -*- mode: ruby -*-
# vi: set ft=ruby :

boxes = [
  { :name => "centos-5", :box => "parallels/centos-5.11" },
  { :name => "centos-6", :box => "parallels/centos-6.7" },
  { :name => "centos-7", :box => "parallels/centos-7.1" }
]

Vagrant.configure("2") do |config|
  boxes.each_with_index do |box, index|
    config.vm.define box[:name] do |b|

      b.vm.box_check_update = false
      b.vm.hostname = box[:name]
      b.vm.box = box[:box]
      b.vm.provider "parallels" do |v|
        v.memory = 256
        v.cpus = 1
      end

      if box[:name] == "centos-5"
        b.vm.provision "shell",
          inline: "yum install -q -y python-simplejson"
      end

      # The last VM is used to provision all VMs at once
      if index == boxes.length - 1
        b.vm.provision "ansible" do |a|
          a.playbook = "test.yml"
          a.limit = 'all'
          a.verbose = 'vv'
        end
      end

    end
  end
end