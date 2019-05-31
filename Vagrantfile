required_plugins = ["vagrant-hostsupdater"]
required_plugins.each do |plugin|
    exec "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

Vagrant.configure("2") do |config|
  config.vm.define "app" do |app|
    app.vm.box = "ubuntu/xenial64"
    app.vm.network "private_network", ip: "192.168.10.100"
    app.hostsupdater.aliases = ["nginx.local"]
    app.vm.provision "chef_solo" do |chef|
      chef.add_recipe "nginx::default"
      chef.add_recipe "python::default"
      chef.version = '14.12.9'
    end
  end
end
