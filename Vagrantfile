VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "atomic"
  config.vm.synced_folder './', '/vagrant', type: 'rsync', disabled: true

  config.vm.provider :virtualbox do |v|
    v.memory = 4096
    v.cpus =4
    v.customize ["modifyvm", :id, "--cpus", "4"]
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  config.vm.provider :libvirt do |libvirt|
    libvirt.cpus = 2
    libvirt.memory = 1024
    libvirt.driver = 'kvm' # needed for kvm performance benefits!
    libvirt.connect_via_ssh = false
    libvirt.username = 'root'
  end

  config.vm.define "atomic-1" do |config|
    config.vm.network "forwarded_port", guest: 43273, host: 50001
    config.vm.network "forwarded_port", guest: 1001, host: 50002
    config.vm.network "forwarded_port", guest: 14000, host: 50003
  end
end
