# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::Config.run do |config|
  config.vm.box       = 'precise32'
  config.vm.box_url   = 'http://files.vagrantup.com/precise32.box'
  config.vm.host_name = 'chef-rails-dev-box'

  config.vm.network :hostonly, "192.168.30.00"
  config.vm.share_folder("vagrant-root", "/vagrant", ".", "nfs" => true)

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = ["chef/cookbooks", "chef/site-cookbooks"]
    chef.roles_path     = [[:host, "chef/roles"]]
    chef.data_bags_path = [[:host, "chef/data_bags"]]

    chef.add_role "rails-development"
    chef.json = {
        :mysql => {
          :server_root_password   => 'toor',
          :server_debian_password => 'toor',
          :server_repl_password   => 'toor'
        },
        "postgresql" => {
          "password" => {
            "postgres" => "toor"
          }
        },
        "rbenv" => {
          "global"  => "ree-1.8.7-2012.02",
          "rubies" => [ "2.0.0-p0", "ree-1.8.7-2012.02" ],
          "gems" => {
            "ree-1.8.7-2012.02" => [
              { 'name' => 'bundler' }
            ],
            "2.0.0-p0" => [
              { 'name' => 'bundler' }
            ]
          }
        }
      }
  end
end
