# servicemix-playbook
Ansible playbook for getting Apache Servicemix ground up on any remote Linux box

## Target of the playbook

This is an ansible playbook that caters pulling down a fresh Apache Servicemix from the distribution,  explode it on the remote box and start the Karaf. Also it serves the purpose of installing various features to the Karaf container once it is up.

## Dynamics of the playbook

* `inventory` file contains the list of the remote linux boxes that we need to confiure servicemix on.
* `play.yml` is the starting point for the ansible where it gets to know what host groups and roles are we 
   going to work on.
* `roles` decribes the tasks that needs to be executed on the remote box sequentially to get the servicemix
   configured and up and running with the wanted features.
* `group_vars` is the placeholder path where variable values can be injected to the ansible on runtime.

## Running 

Execute the below command:

```
ansible-playbook -i inventory play.yml -vv
```

    -i -> switch for providing the inventory file name
    -vv-> runs the ansible command in the verbose mode

## Prerequisites for Ansible

* Ansible needs to be installed on the box where the script needs to be run. Ideally, it would just need to     be present on the box where the CI/CD pipelines are running. It does not need to be there in the developer    machines. 

    https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html

* Here in this sample, I have used AWS EC2 instance that is created with the ssh key. Ansible needs the ssh     public/private key pair for doing ssh into the remote box for performing the tasks.
 
## Feature and Bundle Installs

Feature and bundle installs on the karaf instance gets iterated automatically from a list of features/bundles that we want the karaf instance to have. 

This list is very simple and can be updated just at the variable level and the core playbook does not need to be touched at all. 

## Inventory

Core of ansible is the list of inventories on which the ansible need to iterate through to perform the tasks. It is just a simple file with the IP or the FQDN of the box/server that you need to go through this. 

In future, if the servers go up, all we need to do is to add another entry to the inventory file.
