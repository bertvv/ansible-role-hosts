require 'rbconfig'

ROLE_NAME = 'hosts'
HOST_NAME = 'test' + ROLE_NAME
VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'bertvv/centos72'

  config.vm.define HOST_NAME do |node|
    node.vm.hostname = HOST_NAME
    node.vm.network 'private_network', ip: '192.168.56.56'
    node.vm.provision 'ansible' do |ansible|
      ansible.playbook = 'test.yml'
    end
  end
end

# vi: ft=ruby
