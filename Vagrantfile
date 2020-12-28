Vagrant.configure("2") do |config|
  config.vm.box = "apopa/bionic64"
  config.vm.hostname = "kitchen"
  config.vm.network "public_network", ip: "192.168.178.70", bridge: "wlp0s20f3"
  config.vm.provision "shell", path: "scripts/ruby.sh"
  config.vm.provision "shell", path: "https://raw.githubusercontent.com/andrewpopa/bash-provisioning/main/terraform/latest.sh"
end
