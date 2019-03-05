#### liquidbase - database migration as code

#### liquidbase can be run from ansible

#### -m is a module
 ping or dnf are modules

#### you send arguments to the module with -a 

#### update mechanism 

 -  ansible is push based structure
    - it is agent less model
    - ansible control box can only run on windows - but the cluster can have windows machine

 - chef and puppet work as poll mechanism

#### group of hosts are managed in an inventory file

#### always target a group in your playbook

##### name of the group and the group_vars file should be named the same

hostvars file should be named as the hostname

hostvars override groupvars

### split tiers(dev,prod,intx) as diffrent groups or folder structure


#### roles define the order of tasks to run


has about 1400 modules

## Can be used across multiple cloud instances


### Ansible galaxy can be used to get popular roles 

you can pull the roles from ansible galaxy and runs the tasks 

Always inspect the files before running it. 


## Ansible is owned by redhat which is onwed ny IBM

Jenkins has a plugin for ansible deployment


Ansible has  ansible-vault 
but can be scripted to use hasicorp vault


## Ansible new version does support python 3 (still new)

# Cons
 Debugging is hard


is ansible tower opensource?
can we have webhooks?

