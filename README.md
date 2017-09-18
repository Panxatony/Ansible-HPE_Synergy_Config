# Synergy Configuration with Ansible

A group of ansible scripts produced for an account in DXC.technology for OneView in order to configure the HPE Synergy Server

In this GitHub, it holds the structure of files in order for the Ansible playbooks to work.

## PLAYBOOKS:
All the plabooks are in the path of: roles, where you will see the set of folders. Each folder holds a task folder and a main.yml file within it, which is the playbook itself. In order to get items to work with Ansible Tower, I have commented out the config file and any reference to variable directory. If the preferred manner to run Ansible is natively, the config files will need to be commented back in.

#### Tower run Playbooks:
These playbooks are stored at the repository level, these are structured with the hosts, connections and roles listed as this is the format for Ansible Tower.

## VARIABLES:
If needing a variable file, ensure a 'vars' folder has been created in each folder on the same level as the 'tasks' folder. The actual variable file used for this repository has not been uploaded for security reasons, however an example for how the variable file can be setup is here:

```json
Server_Profile_Name: 'Test Profile'
Serv_b1: 'Server Bay 1'
Network_Name: 'Test Network'
```

## CONFIG FILE:
The actual configuration file used for this repository has not been uploaded for security reasons, however an example for how the config file can be setup is here:

```json
"ip": "0.0.0.0",
"credentials": {
    "userName": "Username",
    "password": "password"
    },
"api_version": 300
```

### TIP:
If wanting to produce Ansible with multiple functions (example delete multiple Ethernet functions), copy the required code and paste directly under and change the relevant details. Ansible will read the playbook and complete the tasks
