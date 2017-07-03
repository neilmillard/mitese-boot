# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Config for the role etc
  # This config will give a jenkins server listening on http://localhost:8080/
  $init_repobranch = 'master'
  $init_repouser = 'neilmillard'
  $init_reponame = 'server-provisioning'
  $init_role = 'jenkins'

  $webport = '8080'
  $hostport = '8080'
  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  # we use centos official
  # https://atlas.hashicorp.com/centos/boxes/7
  config.vm.box = "centos/7"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  #Port for the webserver
  config.vm.network "forwarded_port", guest: $webport, host: $hostport

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # the centos/7 box uses rsync by default, for windows you'll want to disable it
  if Vagrant::Util::Platform.windows? then
    config.vm.synced_folder ".", "/vagrant", disabled: true
  end

  if ENV['init_env']
    $init_env = ENV['init_env']
  else
    puts "Environment variable: 'init_env' is not set, defaulting to 'dev'"
    $init_env = 'dev'
  end


  if ENV['init_repobranch']
    $init_repobranch = ENV['init_repobranch']
  else
    puts "Environment variable: 'init_repobranch' is not set, defaulting to 'master'"
    $init_repobranch = 'master'
  end

  args = "--role #{$init_role} --environment #{$init_env} --repouser #{$init_repouser} --reponame #{$init_reponame} --repobranch #{$init_repobranch}"

  config.vm.provision :shell, :path => 'provision.sh', :args => args
end
