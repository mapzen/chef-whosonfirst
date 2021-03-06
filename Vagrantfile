# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.hostname = 'whosonfirst'

  config.omnibus.chef_version = '11.12.8'
  config.berkshelf.enabled = true
  config.vm.box = 'ubuntu-14.04-opscode'
  config.vm.box_url = 'http://opscode-vm-bento.s3.amazonaws.com/vagrant/virtualbox/opscode_ubuntu-14.04_chef-provisionerless.box'

  config.vm.network "forwarded_port", guest: 8080, host: 8080

  config.vm.provision 'chef_solo' do |chef|
  chef.json = {
    'apt' => {
      'compile_time_update' => true
    },
    'authorization' => {
      'sudo' => {
        'users' => ['vagrant'],
        'passwordless' => true
      }
    },
    'java' => {
      'install_flavor' => 'oracle',
      'jdk_version' => '8',
      'oracle' => {
        'accept_oracle_download_terms' => 'true'
      },
      'jdk' => {
        '8' => {
          'x86_64' => {
            'url' => 'http://download.oracle.com/otn-pub/java/jdk/8u45-b14/jre-8u45-linux-x64.tar.gz',
            'checksum' => '6cb35916c59762c1ea6acdb275f93a94'
          }
        }
      }
    }
  }
  chef.run_list = [
    'recipe[sudo]',
    'recipe[ohai]',
    'recipe[whosonfirst::setup_vagrant]',
  ]
  end
end
