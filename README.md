# Creating an ami with Packer

This is a simple POC for using Packer and Ansible to create a custom Amazon AMI.

This repo contains an example [Packer](https://www.packer.io) template and [Ansible](https://www.ansible.com) task to create an Amazon AMI based on CentOS 7 and hardened with the following projects:
 * https://github.com/dev-sec/ansible-os-hardening
 * https://github.com/dev-sec/ansible-ssh-hardening

The JSON file used is used by Packer to create the ami and upload it to your Amazon account.
Packer will use the variables in the top section of the JSON to find and create an ami based on the values it finds.
The last section of the JSON will update the ami with the newest updates it finds and install Ansible.
_ansible-galaxy_ is used to install the two repo's above ready for Ansible to call the roles.
_harden.yml_ is a simple Ansible playbook to run the roles on the ami

## Prerequisites
 * Amazon CLI
 * Packer
 * Ansible

You need to have logged in via the Amazon CLI, the template will pick up the credentials from the ~/.aws/credentials file. Packer needs to be installed as well, and you can add Ansible too to play with.

## To Run:
Checkout the repo and edit as needed, then:
```bash
$ packer build centos7_hardened.json
```
You can validate the JSON before running to check:
```bash
$ packer validate centos7_hardened.json
```
You can also debug if needed with (eg if you change the search string used to find the base ami):
```bash
$ packer build -debug centos7_hardened.json
```
