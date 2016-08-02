## Requirements
1. Vagrant
2. Ansible 2+
3. VirtualBox

## Instructions
- clone repo
- customize the [number of nodes](https://github.com/jpcarey/es_cluster_vagrant/blob/master/Vagrantfile#L7), default: `N = 3`
- vagrant up

## Other stuff
- You can re-provision an already running cluster. Modify the ansible playbook, and run `vagrant provision`
- You can suspend a cluster, `vagrant suspend`
- The certs are idempotent, and not recreated. Delete the `certs` directory inside of `provisioning` in order to get new certs.
