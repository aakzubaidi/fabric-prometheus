# Installing Node Exporter

## Install Ansible
[Installing Ansible Details](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
TL;DR `sudo dnf install ansible`

## Install Needed Ansible role
`ansible-galaxy install cloudalchemy.node-exporter`

## Set user username/pasword for client auth.

Edit file `users.yml` to contain the username:password for the rack's Prometheus client. 
Use bycrypt (found in apache2-utils or httpd-tools package) to generate the pasword hash. 
Optionally, you can also add any other users that may need access to the exporter's metrics. 

## Set Host
Edit the `hosts` file. Add the host(s) onto which  you will be installing the node exporter. See the file for examples.

## Run Playbook
Below are the commands to run ansible to install the node_exporter software on the head node or worker nodes.  The only difference is the head node is only exposed on the localhost so it does not require a TLS cert or user/password setting.
For either case may optionally add these flags.
* Add `--check` to run without actually making changes on remote host.  
* Add `--ask-pass` if password needed to login to node.  
* Add `--ask-become-pass` if sudo password needed on node. 
### Head Node Exporter
Run the playbook using `ansible-playbook -i hosts node_exporter_localhost_playbook.yml`
### Worker Node Exporters
Run the playbook using `ansible-playbook -i hosts node_exporter_self_signed_cert_playbook.yml`
 





