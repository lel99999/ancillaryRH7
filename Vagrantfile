Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |v|
    v.memory = "1024"
    v.cpus = 2
    v.customize ["modifyvm", :id, "--cpuexecutioncap", "70"]
  end
# config.trigger.after :up do |trigger|
#   run "subscription-manager register --username <username> --password <password> --auto-attach
#   trigger.name = "After-Up Trigger ..."
#   trigger.info = "Trigger Execution ..."
#   trigger.run = { path:"subscription-manager register --username <username> --password <password> --auto-attach"}
# end

  config.vm.define "ancillaryRH7" do |ancillaryRH7|
#   ancillaryRH7.vm.box = "generic/rhel7"
#    ancillaryRH7.vm.box = "RH7.5_base"
    ancillaryRH7.vm.box = "clouddood/RH7.5_baserepo"
    ancillaryRH7.vm.hostname = "ancillaryRH7"
    ancillaryRH7.vm.network "private_network", ip: "192.168.60.149"
    ancillaryRH7.vm.provision "shell", :inline => "sudo echo '192.168.60.189 ancillaryRH7.local ancillaryRH7' >> /etc/hosts"

    # Default
    ancillaryRH7.vm.provision "main", type: "ansible" do |ansible|
      ansible.playbook = "deploy_ancillaryRH7.dev_local"
      ansible.inventory_path = "vagrant_hosts"
      #ansible.tags = ansible_tags
      #ansible.verbose = ansible_verbosity
      #ansible.extra_vars = ansible_extra_vars
      #ansible.limit = ansible_limit
    end
    # Update
    ancillaryRH7.vm.provision "update", type: "ansible" do |ansible|
      ansible.playbook = "deploy_ancillaryPatchRH7.dev_local"
#     ansible.playbook = "deploy_ancillaryRH7.dev_local"
      ansible.inventory_path = "vagrant_hosts"
      #ansible.tags = ansible_tags
      #ansible.verbose = ansible_verbosity
      #ansible.extra_vars = ansible_extra_vars
      #ansible.limit = ansible_limit
    end
  end
# config.trigger.before :destroy do |trigger|
#   run "rm -Rf /tmp/abc/*"
    # subscription-manager remove --all
    # subscription-manager unregister
    # subscription-manager clean
#   trigger.name = "Destroy Trigger ..."
#   trigger.info = "Destroy Trigger Execution ..."
#   trigger.run = { path: "subscription-manager remove --all"}
#   trigger.run = { path: "subscription-manager unregister"}
#   trigger.run = { path: "subscription-manager clean"}
# end
end
