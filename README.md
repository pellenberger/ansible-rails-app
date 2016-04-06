# A small Rails server playbook for Ansible

**Massively based on https://github.com/radar/ansible-rails-app**

## To know

It installs:

- Ruby 2.1.0
- PostgreSQL 9.3
- nginx 1.8.1
- Passenger 5.0.26

This script is designed to create a production environment only.   
Tested on Ubuntu 12.04.5 (precise).   

Inspired by following tutorials (Ruby on Rails deployment) : 
- https://gorails.com/deploy/ubuntu/14.04
- http://ryanbigg.com/2015/07/deploying-a-rails-application-on-ubuntu-passenger-edition/

## Prerequisites

Host machine has a user that is sudoer and SSH-able (with password). User is defined in Ansible script as *ansible_user*.   
A first SSH connection is done before running playbook, and authenticity of host must have been accepted.   

**Tip :**   
Ansible script does a copy of the public key from management machine to host (for *ansible_user*). Therefore, following connections can be done using SSH key authentication. 

## Use

1. Rename `hosts.example` to `hosts`
2. Rename `vars/defaults.yml.example` to `vars/defaults.yml`
3. Replace all `<examples>` with your own values

To run:

    $ ansible-playbook -i hosts playbook.yml --ask-pass --ask-sudo

Passwords for *ansible_user* (defined in `hosts`) and sudo user (on the host machine) will be asked.   

After playbook successfully configured server, add public key of deploy user to project Github repository.

Now deploy app using Capistrano.   

## Capistrano

Rails app can be configured like described in the two tutorials above.   
An example of a simple application can be found here :   
https://github.com/pellenberger/rails-deploy   
