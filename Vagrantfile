# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define :template do |t|
  end

  config.vm.synced_folder "./", "/app/"
  
  config.vm.network "private_network", ip: "192.168.50.99"

  config.vm.provider :virtualbox do |vb|
  	vb.name = "template"
    vb.customize ["modifyvm", :id, "--cpus", "2", "--memory", 2048]
  end

  config.vm.box = "opscode-ubuntu-12.04-chef-11.4.4"
  config.vm.box_url = "https://opscode-vm.s3.amazonaws.com/vagrant/opscode_ubuntu-12.04_chef-11.4.4.box"

  config.berkshelf.enabled = true
  
  config.vm.provision :shell, :inline => "sudo apt-get update -y"
  config.vm.provision :shell, :inline => "sudo locale-gen fi_FI.UTF-8"
  config.vm.provision :shell, :inline => "sudo apt-get install -y libfontconfig"
  
  config.vm.provision :chef_solo do |chef|
    chef.log_level = :debug
    chef.add_recipe "apt"
    chef.add_recipe "locales"
    chef.add_recipe "timezone-ii"
    chef.add_recipe "ntp"
    chef.add_recipe "vim"
    chef.add_recipe "nano"
    chef.add_recipe "curl"
    chef.add_recipe "java"
    chef.add_recipe "maven"
    chef.add_recipe "gradle"
    chef.add_recipe "nodejs"
    chef.add_recipe "golang"
    chef.add_recipe "mongodb::10gen_repo"
    chef.add_recipe "mongodb::default"
    chef.add_recipe "rvm"
    chef.add_recipe "rvm::system"
    chef.add_recipe "rvm::vagrant"
      
    chef.json = {
      :locales => {
        :available => "fi_FI.utf8",
        :default => "fi_FI.utf8"
      },
      :go => {
        :version => "1.2"
      },
      :java => {
        :install_flavor => "oracle",
        :jdk_version => "7",
        :oracle => {
          "accept_oracle_download_terms" => true
        }
      },
      :maven => {
        :version => "3",
        :mavenrc => {
          :opts => "-Dmaven.repo.local=$HOME/.m2/repository -Xmx512m -XX:MaxPermSize=256m"
        }
      },
      :gradle => {
        :version => "1.10",
        :url => "http://services.gradle.org/distributions/gradle-1.10-all.zip"
      },
      :tz => "UTC",
      :nodejs => {
        :install_method => "package",
        :version => "0.10.25"

      },
      :rvm => {
        :rubies => ["ruby-2.1.0"],
        :default_ruby => 'ruby-2.1.0',
        :gems => {
          'ruby-2.1.0' => [
            { 
              'name'    => 'sass',
              'version' => '3.2.13' 
            },
            { 
              'name'    => 'compass',
              'version' => '0.12.2' 
            }
          ]
        }
      }
    }
  end

  config.vm.provision :shell, :inline => "sudo npm install -g yo grunt-cli bower phantomjs generator-angular http-server express"
  config.vm.provision :shell, :inline => "sudo chown -R vagrant:root /opt/go"

end