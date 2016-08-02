Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"

  host_vars = {}
  groups = {"elasticsearch" => [],  "elasticsearch:vars" => {"discovery" => []}}

  N = 3
  (1..N).each do |machine_id|
    config.vm.define "node#{machine_id}" do |machine|

      private_ip = "10.0.0.1#{machine_id}"

      machine.vm.hostname = "node#{machine_id}"
      machine.vm.network "private_network", ip: private_ip
      machine.vm.network "forwarded_port", guest: 9200, host: "920#{machine_id}"

      host_vars[ machine.vm.hostname ] = { "es_instance_name" => machine.vm.hostname }

      groups["elasticsearch"] << machine.vm.hostname
      groups["elasticsearch:vars"]["discovery"] << private_ip

      # Only execute once the Ansible provisioner,
      # when all the machines are up and ready.
      if machine_id == N
        machine.vm.provision :ansible do |ansible|
          # Disable default limit to connect to all the machines
          puts host_vars
          puts groups
          ansible.limit = "all,localhost"
          ansible.playbook = "provisioning/playbook.yml"
          ansible.host_vars = host_vars
          ansible.groups = groups

          # unset this when not testing commands
          # ansible.tags="test2"
          # ansible.verbose = true
        end
      end
    end
  end

end
