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
    config.vm.provision "shell", inline: <<-SHELL
      apt-get update
      test -x /usr/bin/python || apt-get -y install python2.7-minimal
      update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1
    SHELL
    def ip
      puts "/usr/bin/vagrant ssh-config | /bin/grep -i HostName | cut -d ' ' -f4"
    end
#   config.vm.provision "ansible" do |ansible|
#     ansible.playbook = "playbook.yml"
#   end
  end
end
