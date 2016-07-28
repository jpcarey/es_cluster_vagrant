Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  host_vars = {}

  N = 3
  (1..N).each do |machine_id|
    config.vm.define "node#{machine_id}" do |machine|
      machine.vm.hostname = "node#{machine_id}"
      machine.vm.network "private_network", ip: "10.0.0.1#{machine_id}"
      machine.vm.network "forwarded_port", guest: 9200, host: "920#{machine_id}"

      host_vars[ machine.vm.hostname ] = { "es_instance_name" => machine.vm.hostname }

      # Only execute once the Ansible provisioner,
      # when all the machines are up and ready.
      if machine_id == N
        machine.vm.provision :ansible do |ansible|
          # Disable default limit to connect to all the machines
          puts host_vars
          ansible.limit = "all"
          ansible.playbook = "provisioning/playbook.yml"
          ansible.host_vars = host_vars
          # p ansible.host_vars
          # ansible.host_vars = {
          #   machine.vm.hostname => { es_instance_name => machine.vm.hostname }
          # }
          # ansible.host_vars = {
          #   "host1" => {"http_port" => 80,
          #               "maxRequestsPerChild" => 808},
          #
          #   "host2" => {"http_port" => 303,
          #               "maxRequestsPerChild" => 909}
          # }
          # ansible.verbose = true
        end
      end
    end
  end

end
