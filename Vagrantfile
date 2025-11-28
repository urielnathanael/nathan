Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"

  config.vm.boot_timeout = 600
  config.ssh.connect_timeout = 60

  config.vm.network "forwarded_port", guest: 8080, host: 8080

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
    vb.cpus = 2
  end
end
