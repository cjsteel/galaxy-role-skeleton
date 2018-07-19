# -*- mode: ruby -*-
  # vi: set ft=ruby ts=2 sw=2 tw=0 et :
# bump your IPs and include version when adding new boxes
# https://app.vagrantup.com/debian

  role = File.basename(File.expand_path(File.dirname(__FILE__)))
  gui = true

  boxes = [
    {
      :name => "stretch",
      :box => "debian/stretch64",
      :distribution => "debian",
      :version => "9.4.0",
      :ip => '10.0.0.10',
      :cpu => "50",
#      :disk_size => "10GB",
      :ram => "256"
    },
    {
      :name => "precise",
      :box => "ubuntu/precise64",
      :distribution => "ubuntu",
      :version => "20170427.0.0",
      :ip => '10.0.0.11',
      :cpu => "50",
#      :disk_size => "10GB",
      :ram => "256"
    },
    {
      :name => "trusty",
      :box => "ubuntu/trusty64",
      :distribution => "ubuntu",
      :version => "20180510.0.5",
      :ip => '10.0.0.12',
      :cpu => "50",
#      :disk_size => "10GB",
      :ram => "256"
    },
    {
      :name => "xenial",
      :box => "ubuntu/xenial64",
      :distribution => "ubuntu",
      :version => "20180522.0.0",
      :ip => '10.0.0.13',
      :cpu => "50",
#      :disk_size => "10GB",
      :ram => "256"
    },
    {
      :name => "bionic",
      :box => "ubuntu/bionic64",
      :distribution => "ubuntu",
      :version => "20180717.1.0",
#      :version => "20180522.0.0",
      :ip => '10.0.0.13',
      :cpu => "50",
#      :disk_size => "10GB",
      :ram => "256"
    },
    {
      :name => "centos6",
      :box => "centos/6",
      :distribution => "redhat",
      :version => "1804.02",
      :ip => '10.0.0.15',
      :cpu => "50",
#      :disk_size => "10GB",
      :ram => "256"
    },
    {
      :name => "centos7",
      :box => "centos/7",
      :distribution => "redhat",
      :version => "1804.02",
      :ip => '10.0.0.16',
      :cpu => "50",
#      :disk_size => "10GB",
      :ram => "256"
    },
  ]

  Vagrant.configure("2") do |config|
    boxes.each do |box|
      config.vm.define box[:name] do |vms|
        vms.vm.box = box[:box]
 #       vms.disksize.size = box[:disk_size]
        vms.vm.box_version = box[:version]
        vms.vm.guest = box[:distribution]
        vms.vm.hostname = box[:name]
  #      vms.vm.synced_folder ".vagrant/synced", "/home/vagrant"
        vms.vm.provider "virtualbox" do |vbox|
          vbox.gui = gui
          vbox.name = "#{role}-#{box[:name]}"
          vbox.customize ["modifyvm", :id, "--cpuexecutioncap", box[:cpu]]
          vbox.customize ["modifyvm", :id, "--memory", box[:ram]]
        end

        vms.vm.network :private_network, ip: box[:ip]

#        vms.vm.provision "shell",
#          inline: "echo 'up and running'"

        vms.vm.provision "vai" do |ansible|
          ansible.inventory_dir='tests/vagrant'
          ansible.inventory_filename='generated_inventory'
          # optional: add a group listing all vagrant machines
          ansible.groups = {
            'debian' => ["stretch"],
            'ubuntu' => ["xenial", "trusty"],
            'redhat' => ["centos6", "centos7"],
          #  '_provided_by_vagrant_'=> HOSTS.keys,
          }
        vms.vm.provision "shell",
          inline: "echo 'system booted'"
#        end
        vms.vm.provision :ansible do |ansible|
          ansible.playbook = "tests/vagrant/site.yml"
          ansible.verbose = "vv"
        end
      end
    end
  end
end
