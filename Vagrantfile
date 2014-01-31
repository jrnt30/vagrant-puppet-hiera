#!/usr/bin/env ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.require_plugin 'vagrant-librarian-puppet'

Vagrant.configure('2') do |config|
  config.vm.box = 'centos64'
  config.vm.box_url = 'http://puppet-vagrant-boxes.puppetlabs.com/centos-64-x64-vbox4210.box'


  config.librarian_puppet.puppetfile_dir = 'puppet'
  config.librarian_puppet.resolve_options = { :force => true }

  config.vm.provision :puppet do |puppet|
    puppet.module_path = ['puppet/modules','puppet/lib']
    puppet.manifests_path = 'puppet/manifests'
    puppet.manifest_file = 'site.pp'    

    puppet.options = "--hiera_config /vagrant/puppet/manifests/hiera.yaml"
    # Had to add in FACTER variable in order for the data_dir to work properly, due to our reference of it in hiera.yaml
    puppet.facter = {
      "hiera_config" => "/vagrant/puppet/manifests/config"
    }
  end
end