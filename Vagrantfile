Vagrant.configure(2) do |config|
  config.vm.define "apache.vagrant", primary: true, autostart: true do |config_machine|
      #Assigning a provider
      config_machine.vm.provider :virtualbox do |virtualbox, override|
        virtualbox.name = "Vagrant Apache"
        #override.vm.box = "chef/centos-7.0"
        override.vm.box = "ubuntu/trusty64"

        # Configuring network
        override.vm.network "forwarded_port", guest: 80, host: 8080, auto_correct: true
        override.vm.network "forwarded_port", guest: 443, host: 8443, auto_correct: true
      end
	  
      # Asinging a provisioner
      config_machine.vm.provision :ansible, run: "always" do |provisioner|
        provisioner.playbook = "build/playbook.yml"
        provisioner.extra_vars = "build/settings.yml" if File.file?("settings.yml")
        provisioner.vault_password_file = ".vault.txt" if File.file?(".vault.txt")
      end
  end
end