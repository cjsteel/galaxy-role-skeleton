# -*- mode: ruby -*-
  # vi: set ft=ruby ts=2 sw=2 tw=0 et :
# bump your IPs and include version when adding new boxes
# https://app.vagrantup.com/debian

  role = File.basename(File.expand_path(File.dirname(__FILE__)))
  gui = true

  boxes = [
    {
      :name => "stretch",
      :distribution => "debian",
      :box => "debian/stretch64",
      :version => "9.4.0",
#      :box => "natx/debian-stretch-amd64-desktop",
#      :version => "0.0.5",
      :ip => '10.0.0.10',
      :cpu => "50",
#      :disk_size => "10GB",
      :ram => "256"
    },
    {
      :name => "jessie",
      :distribution => "debian",
      :box => "debian/stretch64",
      :version => "9.4.0",
#      :box => "gtemgoua/debian-dev-workstation",
#      :version => "0.0.1",
      :ip => '10.0.0.11',
      :cpu => "50",
#      :disk_size => "10GB",
      :ram => "256"
    },
    {
      :name => "precise",
      :distribution => "ubuntu",
      :box => "ubuntu/precise64",
      :version => "20170427.0.0",
#      :box => "box-cutter/ubuntu1204-desktop",
#      :version => "2.0.26",
      :ip => '10.0.0.21',
      :cpu => "50",
#      :disk_size => "10GB",
      :ram => "256"
    },
    {
      :name => "trusty",
      :distribution => "ubuntu",
      :box => "ubuntu/trusty64",
      :version => "20180510.0.5",
#      :box => "box-cutter/ubuntu1404-desktop",
#      :version => "2.0.26",
      :ip => '10.0.0.22',
      :cpu => "50",
#      :disk_size => "10GB",
      :ram => "256"
    },
    {
      :name => "xenial",
      :distribution => "ubuntu",
      :box => "ubuntu/xenial64",
      :version => "20180522.0.0",
#      :box => "jcaraballo/ubuntu-desktop-xenial",
#      :version => "0.0.3",
      :ip => '10.0.0.23',
      :cpu => "50",
#      :disk_size => "10GB",
      :ram => "256"
    },
    {
      :name => "bionic",
      :distribution => "ubuntu",
      :box => "ubuntu/bionic64",
      :version => "20180717.1.0",
#      :version => "20180522.0.0",
#      :box => "teknikersai/ubuntu-desktop-bionic64",
#      :version => "0.0.2",
      :ip => '10.0.0.24',
      :cpu => "50",
#      :disk_size => "10GB",
      :ram => "256"
    },
    {
      :name => "centos6",
      :distribution => "redhat",
      :box => "centos/6",
      :version => "1804.02",
#      :box => "Mitsutoshi-NAKANO/CentOS6jaDesktop",
#      :version => "0.6.0",
      :ip => '10.0.0.31',
      :cpu => "50",
#      :disk_size => "10GB",
      :ram => "256"
    },
    {
      :name => "centos7",
      :distribution => "redhat",
      :box => "centos/7",
      :version => "1804.02",
#      :box => "dalmait/centos7",
#      :version => "0.1.8",
      :ip => '10.0.0.32',
      :cpu => "50",
#      :disk_size => "10GB",
      :ram => "256"
    },
  ]

  Vagrant.configure("2") do |config|
    boxes.each do |box|
#      config.vbguest.auto_update = true
#     https://github.com/dotless-de/vagrant-vbguest
#     run something like this:
#     mkdir ~/resources/sw/ubuntu/16.04/virtualbox/5.2.16
#     wget http://download.virtualbox.org/virtualbox/5.2.16/VBoxGuestAdditions_5.2.16.iso
#     then the config.vbguest.iso_path below will work:
#
      config.vbguest.iso_path = "#{ENV['HOME']}/resources/sw/ubuntu/16.04/virtualbox/%{version}/VBoxGuestAdditions_%{version}.iso"
#      config.vbguest.iso_upload_path = "/tmp"
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
