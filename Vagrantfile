# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "digital_ocean"

  config.vm.define "droplet-name" do |config|
    config.vm.provider :digital_ocean do |provider, override|
      override.ssh.private_key_path = '~/.ssh/id_rsa'
      override.vm.box = 'digital_ocean'
      override.nfs.functional = false
      provider.token = ENV['do_token']
      provider.image = 'ubuntu-16-04-x64'
      provider.region = 'nyc1'
      provider.size = '512mb'
    end

  config.vm.synced_folder ".", "/vagrant", disabled: true

    config.vm.provision "shell", inline: <<-SHELL
      DEBIAN_FRONTEND=noninteractive
      export LANGUAGE=en_US.UTF-8
      export LANG=en_US.UTF-8
      export LC_ALL=en_US.UTF-8
      locale-gen en_US.UTF-8
      dpkg-reconfigure locales
      apt-get update
      test -x /usr/bin/python || apt-get -y install python2.7-minimal
      update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1
    SHELL


    config.vm.provision "ansible" do |ansible|
      ansible.extra_vars = {
        site: "go.aaaj.ru",

        letsencrypts_email: "tty8747@gmail.com",

        update_cache: "yes",
        cache_valid_time: "86400",

        worker_connections: "768",

        phpFpmVersion: "7.0",
        phpFpmListen: "/run/php/php7.0-fpm.sock",

        locationPhpFpmApp: "/api/diff/",
        locallocationPhpFpmApp: "/srv/phpapp/",

        locationHtmlApp: "/",
        localLocationHtmlApp: "/srv/www",
   
        locationGoApi: "/api/sum/",
        localLocationGoApi: "/srv/goapi",
      }

      ansible.galaxy_role_file = 'requirements.yml'
      ansible.playbook = "init.yml"
      ansible.playbook = "deploy.yml"
    end
  end
end
