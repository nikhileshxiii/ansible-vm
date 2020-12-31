ENV['VAGRANT_DEFAULT_PROVIDER'] = 'virtualbox'

Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu2004"
  config.ssh.insert_key = false
  config.vm.box_check_update = true

  config.vm.synced_folder ".", "/home/vagrant/", owner: 'vagrant', group: 'vagrant'

  config.vm.provider "libvirt" do |vb|
    # vb.cpus = 2
    # vb.nested = true
    # vb.memory = "8192"
    vb.memory = "1024"
  end


  config.vm.provider "virtualbox" do |vb|
    # vb.gui = true
    vb.memory = "4096"
  end


  config.vm.define "ubuntumachine" do | local |
    local.vm.hostname = "ubuntumachine"
    # local.vm.network :private_network, :ip => "192.168.60.4"

    config.vm.provision "shell", inline: <<-SHELL
      sudo apt update -y
      sudo apt install -y python3 python3-pip python3-venv ansible
    SHELL

    config.vm.provision "ansible" do |ansible|
      ansible.limit = "all"
      # ansible.inventory_path = "inventory"
      ansible.playbook = "play.yml"
      ansible.extra_vars = { ansible_python_interpreter:"/usr/bin/python3" }
    end
  end
end
