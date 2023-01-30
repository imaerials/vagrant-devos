load 'variables.rb'
Vagrant.configure("2") do |config|
    config.vm.box = "generic/ubuntu2204"
    config.vm.provider "vmware_desktop" do |v|
      v.vmx["memsize"] = "4096"
      v.vmx["numvcpus"] = "2"
      v.vmx["displayname"] = "ubuntu-dev"
    end
    config.vm.synced_folder Dir.pwd, "/home/vagrant", type: "smb",smb_username: VAGRANT_SMB_USERNAME, smb_password: VAGRANT_SMB_PASSWORD
    config.vm.network "forwarded_port", guest: 80, host: 8080
    config.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.install_mode = "pip"
      ansible.provisioning_path = "/home/vagrant"
      ansible.tags = "osupdate"
    end
end
