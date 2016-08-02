## Description
The goal is to provision a fully working elasticsearch cluster with encryption. Currently it sets up a CA & Intermediate, and creates certs for each node (truststore and keystore).

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

## Features in Progress
- Add LDAP role to control users and groups for Shield
- Configure Shield PKI auth, and setup client certs
- Add a optional VM with Kibana (plus SSL) & Logstash (using client certs)
- Kibana should have all plugins installed (Shield, Graph, Marvel, Timelion)
- Logstash should populate some sample data to elasticsearch (something like makelogs?, open to ideas)
- Create an example vagrant provisioner for AWS testing (my poor laptop battery will love this)
