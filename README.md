# Windows環境用 Vagrantfile

Vagrant.configure("2") do |config|
  # Virtual OS
  config.vm.box = "centos/7"

  # PrivateIP
  config.vm.network "private_network", ip: "192.168.33.10"

  # Synced Folder
  config.vm.synced_folder "./docker", "/home/vagrant/docker", type:"virtualbox", mount_options: ['dmode=777','fmode=777']

  # Provisioning Script
  config.vm.provision :shell, :path => "provision.sh"

  config.vm.provider "virtualbox" do |vm|
    # メモリを1024MBに設定
    vm.memory = 2048
  end

  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = false
  end

end
