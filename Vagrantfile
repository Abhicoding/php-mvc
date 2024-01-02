
VAGRANT_HOST_NAME = "my.mvc-local.dev"
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.box_check_update = "false"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.cpus = 2
   end
   config.vm.hostname = VAGRANT_HOST_NAME
   config.vm.provision "shell", inline: "sudo hostnamectl set-hostname my.mvc-local.dev"
   config.vm.network "private_network", ip: "192.168.50.4"
   config.vm.synced_folder ".", "/vagrant/application", owner: "vagrant", group: "vagrant"
   #  Server port
   config.vm.network :forwarded_port, guest: 80, host: 8080, auto_correct: true
   # MySQL port
   config.vm.network :forwarded_port, guest: 3306, host: 3306, auto_correct: true
  # Provisioning configuration for Ansible (for Mac/Linux hosts).
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
    ansible.inventory_path = "provisioning/inventory"
    # ansible.become = true
    ansible.limit = VAGRANT_HOST_NAME
    ansible.compatibility_mode = "2.0" # Specify Ansible compatibility mode
  end
  # config.vm.provision :shell, :path => "start.sh", run: "always"
end