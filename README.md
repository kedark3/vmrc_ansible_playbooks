# vmrc_ansible_playbooks
Ansible playbooks to automate the browser setup for vmrc
This project contains 4 primary roles: 
- Installing Firefox on Linux 
- Installing Chrome on Fedora
- Installing Chrome on RHEL
- Installing VMRC Remote Console Plugin on Linux using .bundle installation file

All of these roles are included in the main playbook main.yaml in the root directory of the project. 

# Role Structure 
Every role in this project follows a simple directory structure in which it may have following directories: 
- **/defaults**: Includes main.yaml file which holds the default values of the variables that the role will require and
  it can be overridden by using --extra-vars on the command line at the time of execution of playbook. 
- **/tasks**: Includes main.yaml tasks file, listing out all the tasks that are carried by the role 

## Running the Playbook
```sh
ansible-playbook main.yaml
```
This will run the playbook on all the hosts in inventory, i.e. vmrc-linux. See hosts section for more info. 

# Hosts file 

Hosts file contains list of all hosts and it is also known as inventory file to some people. It has been divided into 4 sections:
- vmrc-linux:children - This section is parent section for all other sections. 
- vmrc-rhel - This section will list all the hosts that have RHEL OS. 
- vmrc-fedora - This section will list all the hosts that have Fedora OS. 
- local -If you have any VMs running locally on your computer or want to run the playbook against localhost, then those IP addresses coud be mentioned in this section. 

**NOTE**: vmrc-rhel & vmrc-fedora disctinction is required because when installing Chrome on RHEL we need to subscribe to Red Hat Network and for Fedora we don't. 

To limit execution of playbook against particular group of hosts instead of running against all you can use something like the following command: 

```sh
ansible-playbook main.yaml -l vmrc-rhel
```    
where -l : limit to the particular hosts/host group 

You could also run the playbook against hosts that belong to particular subnet/IP range as:

```sh
ansible-playbook main.yaml -l 10.8.*
```  

## Ansible.cfg 
This repo has own ansible.cfg file which overrides global ansible.cfg file. It mostly has all the required options and you do not need to worry about anything
in this file. File is also very well commented and you can read and modify it to conform your requirements.Funny thing that this file does is 
that it allows all cowsay stencils from cow_whitelist, so every task has a different animal/character cowsay. 
