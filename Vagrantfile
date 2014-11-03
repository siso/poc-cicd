# -*- mode: ruby -*-
# vi: set ft=ruby :
# This is a Vagrant configuration file. It can be used to set up and manage
# virtual machines on your local system or in the cloud. See http://downloads.vagrantup.com/
# for downloads and installation instructions, and see http://docs.vagrantup.com/v2/
# for more information and configuring and using Vagrant.

Vagrant.configure("2") do |config|

  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "hashicorp/precise32"

    # Install Chef on VMs
    config.vm.provision :shell, :inline => "curl -L https://www.opscode.com/chef/install.sh | bash"

    config.vm.define :jenkins do |jenkins|
        jenkins.ssh.forward_agent = true
        #jenkins.vm.synced_folder ".", "/vagrant", :nfs => true
        #jenkins.vm.host_name = "poc-cicd-jenkins"
        config.vm.provision :chef_solo do |chef|
            chef.add_recipe "apt"
            chef.add_recipe "jenkins"
        end
        config.vm.network "forwarded_port", guest: 8080, host: 18080
    end

    config.vm.define :web do |web|
        web.ssh.forward_agent = true
        #web.vm.synced_folder ".", "/vagrant", :nfs => true
        #web.vm.host_name = "poc-cicd-web"
        config.vm.provision :chef_solo do |chef|
            chef.add_recipe "apt"
            chef.add_recipe "apache"
        end
        config.vm.network "forwarded_port", guest: 80, host: 10080
    end

end
