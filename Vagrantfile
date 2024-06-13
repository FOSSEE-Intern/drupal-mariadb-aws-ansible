Vagrant.configure("2") do |config|
  config.vm.box = "generic/alma9"
  config.vm.network :forwarded_port, guest: 80, host: 8080, host_ip: "127.0.0.1", guest_ip: "0.0.0.0"
  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "deploy.yml"
  end
end
