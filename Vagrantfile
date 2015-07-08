# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'ubuntu/trusty64'

  # Allow the project directory to be accessible inside the Vagrant box.
  # This should match the Ansible host_vars/vagrant synced_folder value.
  config.vm.synced_folder '.', '/mnt/vagrant'

  # Ideally, this IP will be unique, so the entry added to /etc/hosts won't
  # conflict with that of another project.
  config.vm.network :private_network, ip: '192.168.33.99'

  # Automatically add an entry to /etc/hosts for this Vagrant box (requires
  # sudo). This should match the Ansible host_vars/vagrant site_fqdn value.
  config.hostsupdater.aliases = ['deployment-workflow.loc']

  # A specific name looks much better than "default" in ansible output.
  config.vm.define 'vagrant'

  # The Vagrant ansible provisioner is used here for convenience. Instead of
  # the following code, the Vagrant box may be provisioned manually with
  # ansible-playbook (like in production), but adding this code saves the
  # trouble of having to run ansible-playbook manually after "vagrant up".
  config.vm.provision 'ansible' do |ansible|
    # Run init playbook (which runs base, configure, link playbooks).
    ansible.playbook = 'deploy/ansible/init.yml'
  end
end
