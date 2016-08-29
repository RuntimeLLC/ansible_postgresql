Vagrant.require_version ">= 1.8.5"

Vagrant.configure("2") do |config|

  # VirtualBox defaults
  config.vm.provider "virtualbox" do |v|
    v.gui = false
    v.name = "postgres"
    v.memory = 1024
    v.cpus = 1
  end

  # Base box
  config.vm.box = "ubuntu/xenial64"

  # Base box url
  config.vm.box_url = "https://vagrantcloud.com/ubuntu/boxes/xenial64"

  # Private network
  config.vm.network "private_network", ip: "192.168.122.201"

  # Hostname
  config.vm.hostname = "postgres"

  #Shell provision
  config.vm.provision "shell",
    inline: "test -f /usr/bin/python || ( apt-get update && apt-get install -y python2.7 && ln -s /usr/bin/python2.7 /usr/bin/python)"

  # Ansible provision
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = ".test.yml"
    ansible.limit = "all"
  end

end
