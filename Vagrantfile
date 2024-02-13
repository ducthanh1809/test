Vagrant.configure("2") do |config|
    config.vm.box = "bento/ubuntu-20.04-arm64"
    (1..1).each do |machine_id|
        config.vm.define "Sv2#{machine_id}" do |cfg|
            cfg.vm.hostname = "sv#{machine_id}"
            cfg.vm.provider :vmware_desktop do |v|
                v.vmx["memsize"] = "10240"
                v.vmx["numvcpus"] = "6"
            end
            cfg.vm.network "public_network", bridge: "ens0"
            cfg.vm.network "private_network", ip: "192.168.88.184"
            cfg.vm.provision :shell, inline: <<-SHELL 
            echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCjFl/TBKVZYb/BSTeEXvNRR5cW+inDVHNkXBftFSZZigaTnClNU1fImhRw4tohP9yOJULyLEdP7RVHgPVKdsfzRmHx+vc7ztzEfQ/gWXUaQJItCggJuKkbBHAi2dZpNgT8arKX1ztQ6dB+SbGKj7hDGmq0TX2fsY2ddYOpZglchxzNZxyXoha+ISc5ilFFiQNc14ej5keZuREl8rXbxGbnKNx3DiW4z0tgbOSdiDWvuOAzymh9wVdSaImdPuLoFTtgimczvLG2r20cZvGOWuVQf2d5lDtGUKzI2wRIYojRpvEiHC+A+Lcu+4uTV3N1oMyCsoxebpF+JJVxuiQu3ROghAXjKAiXvatgdGVv5CpLnpcG2PIcEYVaAQpsSBhog/O0s35S2TFzKgSbEjC+riD6eApwsU7dZesBHGBiBBC+PW2ZGR4THymdVA2VfSeoHJb4nv0WzZUIgQJHpRwwWMyDc8CPra1cjcgqu7tITfy/heh/xRrunkpb6KRqY2W4hxU= du.nguyen@XD4D09K2L6
" >> /home/vagrant/.ssh/authorized_keys
            SHELL
            config.vm.provision 'ansible' do |ansible|
                ansible.playbook = 'playbook.yml'
                ansible.limit = 'all'
                ansible.verbose = 'v'
            end
        end         
    end
end