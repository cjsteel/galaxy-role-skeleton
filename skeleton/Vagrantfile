# -*- mode: ruby -*-
  # vi: set ft=ruby ts=2 sw=2 tw=0 et :
# bump your IPs and include version when adding new boxes
# https://app.vagrantup.com/debian

  role = File.basename(File.expand_path(File.dirname(__FILE__)))

  boxes = [
    {
      :name => "stretch64",
      :box => "debian/stretch64",
      :version => "9.4.0",
      :ip => '10.0.0.10',
      :cpu => "50",
      :ram => "256"
    },
    {
      :name => "precise64",
      :box => "ubuntu/precise64",
      :version => "20170427.0.0",
      :ip => '10.0.0.11',
      :cpu => "50",
      :ram => "256"
    },
    {
      :name => "trusty64",
      :box => "ubuntu/trusty64",
      :version => "20180510.0.5",
      :ip => '10.0.0.12',
      :cpu => "50",
      :ram => "256"
    },
    {
      :name => "xenial64",
      :box => "ubuntu/xenial64",
      :version => "20180522.0.0",
#      :version => "20171221.0.0",
      :ip => '10.0.0.13',
      :cpu => "50",
      :ram => "256"
    },
    {
      :name => "bionic64",
      :box => "ubuntu/bionic64",
      :version => "20180522.0.0",
      :ip => '10.0.0.13',
      :cpu => "50",
      :ram => "256"
    },
    {
      :name => "centos6",
      :box => "centos/6",
      :version => "1804.02",
      :ip => '10.0.0.15',
      :cpu => "50",
      :ram => "256"
    },
    {
      :name => "centos7",
      :box => "centos/7",
      :version => "1804.02",
      :ip => '10.0.0.16',
      :cpu => "50",
      :ram => "256"
    },
  ]

  Vagrant.configure("2") do |config|
    boxes.each do |box|
      config.vm.define box[:name] do |vms|
        vms.vm.box = box[:box]
        vms.vm.box_version = box[:version]
        vms.vm.hostname = box[:name]
  #      vms.vm.synced_folder ".vagrant/synced", "/home/vagrant"
        vms.vm.provider "virtualbox" do |vbox|
          vbox.name = "ansible-#{role}-#{box[:name]}"
          vbox.customize ["modifyvm", :id, "--cpuexecutioncap", box[:cpu]]
          vbox.customize ["modifyvm", :id, "--memory", box[:ram]]
        end

        vms.vm.network :private_network, ip: box[:ip]

        vms.vm.provision "shell",
          inline: "echo 'up and running'"


        vms.vm.provision :ansible do |ansible|
          ansible.playbook = "tests/vagrant.yml"
          ansible.verbose = "vv"
        end
      end
    end
  end
