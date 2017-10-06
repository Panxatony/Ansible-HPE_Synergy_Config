# Synergy Configuration with Ansible

A group of ansible scripts produced for an account in DXC.technology for OneView in order to configure the HPE Synergy Server

In this GitHub, it holds the structure of files in order for the Ansible playbooks to work.

## Required SDKs and tools
Here are a list of SDKs or plugins required to complete all or most of the Playbooks in this repository. 'sudo' installs the tool globally. Without it, then the tool will only download to the local user

### OpenSSH
```json
$ sudo apt-get install openssh-server
$ sudo service ssh status
```

### Ansible
```json
$ sudo apt-get install libssl-dev
$ sudo pip install ansible
```
To check version:
```json
$ pip list
```
### Python and Pip
```json
$ sudo apt-get install python python-pip
```
To check versions:
```json
$ python --version
$ pip --version
```
### unzip
This tool is to literally unzip downloaded packages with the extension of '.zip'
```json
$ sudo apt-get install unzip
```
To check version:
```json
$ pip list
```

### HP OneView
First the packages need to be downloaded
```json
$ wget https://github.com/HewlettPackard/python-hpOneView/archive/master.zip
$ wget https://github.com/HewlettPackard/oneview-ansible/archive/master.zip
```
Then rename the packages to something sensible (otherwise they will be the same). I chose ansible-master.zip and python-master.zip. Whatever they are named, now they need to be unzipped
```json
$ unzip python-master.zip
$ unzip ansible-master.zip
```
Now to install
```json
$ cd python-hpOneView-3.2.2/ #Or whatever the python one is called after unzipping
$ sudo pip install .
```
To check version:
```json
$ pip list
```

### HP ICsp
```json
$ git clone https://github.com/HewlettPackard/python-hpICsp.git
$ cd python-hpICsp
$ sudo pip install .
```
To check version:
```json
$ pip list
```

### HP ILO
The HP ILO module is required to attach an ISO to a profile
```json
$ sudo add-apt-repository ppa:dennis/python
$ sudo apt-get update
$ sudo apt-get install python-hpilo
```
To check version:
```json
$ pip list
```

### Change Environment Variables
Both paths need to be exported otherwise the modules will not work properly
```json
$ export ANSIBLE_LIBRARY=/home/hoppert/oneview-ansible-master/library/
$ export PYTHONPATH=/home/hoppert/python-hpOneview-master:/home/hoppert/oneview-ansible-master/library
```

## PLAYBOOK Information:
All the plabooks are in the path of: roles, where you will see the set of folders. Each folder holds a task folder and a main.yml file within it, which is the playbook itself. In order to get items to work with Ansible Tower, I have commented out the config file and any reference to variable directory. If the preferred manner to run Ansible is natively, the config files will need to be commented back in.

#### Tower run Playbooks:
These playbooks are stored in the Tower Playbooks folder, these are structured with the hosts, connections and roles listed as this is the format for Ansible Tower. They all reference the playbooks below

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
"image_streamer_ip": "0.0.0.1", #If an Image Stream has been installed
"credentials": {
    "userName": "Username",
    "password": "password"
    },
"api_version": 300
```
Remember this needs to be named as 'config.json'

### TIP:
If wanting to produce Ansible with multiple functions (example delete multiple Ethernet functions), copy the required code and paste directly under and change the relevant details. Ansible will read the playbook and complete the tasks

## Ansible structure
There are many ways to structure Ansible, however this is the form I found worked well (when using native Ansible):
- Inventory folder (holds hosts file)
- Roles folder (all playbooks)
- ansible.cfg (sets default parameters)
- config.json (sets configuration details)
- site.retry (just says 'localhost')
- site.yml (Playbook to run anything within roles folder)

## PLAYBOOKS:
A list of Playbooks in this repository, they can also be found in the roles folder:

#### Add/Create Playbooks
- [Appliance Time and Locale Configuration](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Appliance_Time_and_Locale_Configuration/tasks/main.yml)
- [Attach ISO disk to ILO and server bay](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Attach_disk_to_ILO/tasks/main.yml)
- [Create a basic volume disk (100Gb)](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Basic_Disk_Template/tasks/main.yml)
- [Create a server profile with ISO attached](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Basic_Server_Profile_with_iso_disk_attached/tasks/main.yml)
- [Create a large amount of networks, a mixture of Ethernet and Fibre Channel](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Current_Network_Setup/tasks/main.yml)
- [Create a volume disk template for License Cluster](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Disk_Template_for_License_Cluster/tasks/main.yml)
- [Create ESXi 6.5 Server Profile with Image Streamer](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_ESXi_6.5_Profile/tasks/main.yml)
- [Create Enclosure Group](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Enclosure_Group/tasks/main.yml)
- [Create Enhanced volume disk template (20Gb)](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Enhanced_Disk_Template/tasks/main.yml)
- [Create Ethernet Network](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Ethernet_Network/tasks/main.yml)
- [Create Ethernet Network associated to IPv4 subnet](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Ethernet_Network_Associated_to_IPv4_Subnet/tasks/main.yml)
- [Create Ethernet network in bulk with same suffix](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Ethernet_Network_Bulk_with_same_suffix/tasks/main.yml)
- [Create Fibre Channel Network](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Fibre_Channel_Networks/tasks/main.yml)
- [Create Full Enclosure Provision](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Full_provision/tasks/main.yml)
- [Create ICsp Server Profile, Server and Deploy OS](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_ICsp_Profile%2C_Server_and_deploy_OS/tasks/main.yml)
- [Create ICsp Server](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_ICsp_Server/tasks/main.yml)
- [Create Image Streamer Build Plan](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Image_Streamer_Build_Plan/tasks/main.yml)
- [Create Image Streamer Deployment Plan](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Image_Streamer_Deployment_Plan/tasks/main.yml)
- [Create Image Streamer Golden Image](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Image_Streamer_Golden_Image/tasks/main.yml)
- [Create Image Streamer OpenShift InfraNode Profile](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Image_Streamer_OpenShift_InfraNode_Profile/tasks/main.yml)
- [Create Image Streamer OpenShift Master Profile](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Image_Streamer_OpenShift_Master_Profile/tasks/main.yml)
- [Create Image Streamer OpenShift Node 1 Profile](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Image_Streamer_OpenShift_Node1_Profile/tasks/main.yml)
- [Create Image Streamer OpenShift Node 2 Profile](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Image_Streamer_OpenShift_Node2_Profile/tasks/main.yml)
- [Create Image Streamer OpenShift RHEL 7.3 Profile](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Image_Streamer_OpenShift_RHEL7.3_Profile/tasks/main.yml)
- [Create IPv4 Ranges](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_IPv4_Ranges/tasks/main.yml)
- [Create IPv4 Subnet](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_IPv4_Subnet/tasks/main.yml)
- [Create IPv4 Subnet & Ranges](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_IPv4_Subnet_%26_Range/tasks/main.yml)
- [Create Logical Enclosure](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Logical_Enclosure/tasks/main.yml)
- [Create Logical Interconnect Group](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Logical_Interconnect_Group/tasks/main.yml)
- [Create Network Sets](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Network_Sets/tasks/main.yml)
- [Create Network Template for Customer VLAN203](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Network_Template_for_Customer_VLAN203/tasks/main.yml)
- [Create Network Template for License clusters with Trunked VLANs](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Network_Template_for_License_clusters_with_Trunked_VLANs/tasks/main.yml)
- [Create Private Storage Volume](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Private_Storage_Volume/tasks/main.yml)
- [Create Profile with Template and Deployment Plan](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Profile_with_Template_and_Deployment_Plan/tasks/main.yml)
- [Create SAN Manager](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_SAN_Manager/tasks/main.yml)
- [Create Server Profile Template](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Server_Profile_Template/tasks/main.yml)
- [Create Server Profile from Private SAN](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Server_Profile_from_Private_SAN/tasks/main.yml)
- [Create Server Profile via Template](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Server_Profile_via_Template/tasks/main.yml)
- [Create Server Profile with Local Storage](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Server_Profile_with_Local_Storage/tasks/main.yml)
- [Create Shareable Volume](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Shareable_Volume/tasks/main.yml)
- [Create Standard Disk Template](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Standard_Disk_Template/tasks/main.yml)
- [Create Storage Systems with Pools](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Storage_Systems_with_Pools/tasks/main.yml)
- [Create Storage Volume Template](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_Storage_Volume_Template/tasks/main.yml)
- [Create User](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Create_User/tasks/main.yml)

#### Update Playbooks
- [Update Ethernet Network with Associating a Subnet](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Update_Ethernet_Network_with_Associating_a_Subnet/tasks/main.yml)
- [Update Ethernet Network with Removing Subnet](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Update_Ethernet_Network_with_Removing_Subnet/tasks/main.yml)
- [Update Profile with SAN](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Update_Profile_with_SAN/tasks/main.yml)
- [Update Subnet with new Domain](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Update_Subnet_with_new_Domain/tasks/main.yml)
- [Update User Password](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Update_User_Password/tasks/main.yml)

#### Gather facts Playbooks
- [Gather Appliance Time and Locale Configuration](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_Appliance_Time_and_Locale_Config/tasks/main.yml)
- [Gather Enclosure Facts](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_Enclosure_Facts/tasks/main.yml)
- [Gather Enclosure Group URIs](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_Enclosure_Group_Uris/tasks/main.yml)
- [Gather Enclosure Groups](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_Enclosure_Groups/tasks/main.yml)
- [Gather Ethernet Networks](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_Ethernet_Networks/tasks/main.yml)
- [Gather Fibre Channel Networks](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_FC_Networks/tasks/main.yml)
- [Gather Hardware Facts](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_Hardware_Facts/tasks/main.yml)
- [Gather Image Streamer Artifact Bundle](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_Image_Streamer_Artifact_Bundle/tasks/main.yml)
- [Gather Image Streamer Build Plans](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_Image_Streamer_Build_Plans/tasks/main.yml)
- [Gather Image Streamer Deployment Plan](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_Image_Streamer_Deployment_Plan/tasks/main.yml)
- [Gather Image Streamer Golden Image](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_Image_Streamer_Golden_Image/tasks/main.yml)
- [Gather Image Streamer OS Volumes](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_Image_Streamer_OS_Volumes/tasks/main.yml)
- [Gather Image Streamer Plan Scripts](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_Image_Streamer_Plan_Scripts/tasks/main.yml)
- [Gather Logical Interconnect Group](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_Logical_Interconnect_Group/tasks/main.yml)
- [Gather Profile Template](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_Profile_Template/tasks/main.yml)
- [Gather SAN URIs](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_SAN_Uris/tasks/main.yml)
- [Gather SANs](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_SANs/tasks/main.yml)
- [Gather Server Profile from Bay](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_Server_Profile_from_Bay/tasks/main.yml)
- [Gather Server Profiles](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_Server_Profiles/tasks/main.yml)
- [Gather Storage Pools](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_Storage_Pools/tasks/main.yml)
- [Gather Users](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_Users/tasks/main.yml)
- [Gather Volume Template](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_Volume_Template/tasks/main.yml)
- [Gather Volumes](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_Volumes/tasks/main.yml)
- [Gather ALL Network URIs](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Gather_all_Network_Uris/tasks/main.yml)

#### Other Playbooks
- [Download Artifact Bundle](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Download_Artifact_Bundles/tasks/main.yml)
- [Ensure IPv4 Range is Disabled](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Ensure_IPv4_Range_is_Disabled/tasks/main.yml)
- [Ensure IPv4 Range is Enabled](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Ensure_IPv4_Range_is_Enabled/tasks/main.yml)
- [ICsp OS Deployment](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/ICsp_OS_Deployment/tasks/main.yml)
- [Image Streamer Artifact Bundle Download and Upload](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Image_Streamer_Artifact_Bundle_Download_%26_Upload/tasks/main.yml)
- [Image Streamer Upload & Extract Artifact Bundle](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Image_Streamer_Upload_%26_Extract_Artifact_Bundle/tasks/main.yml)
- [Momentary Press Power Off Server](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Momentory_Press_Power_Off_Server/tasks/main.yml)
- [Momentary Press Power On Server](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Momentory_Press_Power_On_Server/tasks/main.yml)
- [Press and Hold Power Off Server](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Press_and_Hold_Power_Off_Server/tasks/main.yml)

#### Delete Playbooks
- [Delete Enclosure Groups](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Delete_Enclosure_Groups/tasks/main.yml)
- [Delete Ethernet Network](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Delete_Ethernet_Network/tasks/main.yml)
- [Delete Fibre Channel Network](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Delete_Fibre_Channel_Network/tasks/main.yml)
- [Delete IPv4 Range](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Delete_IPv4_Range/tasks/main.yml)
- [Delete IPv4 Subnet](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Delete_IPv4_Subnet/tasks/main.yml)
- [Delete IPv4 Subnet & Range](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Delete_IPv4_Subnet_%26_Range/tasks/main.yml)
- [Delete Image Streamer Artifact Bundle](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Delete_Image_Streamer_Artifact_Bundle/tasks/main.yml)
- [Delete Image Streamer Build Plan](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Delete_Image_Streamer_Build_Plan/tasks/main.yml)
- [Delete Image Streamer Deployment Plan](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Delete_Image_Streamer_Deployment_Plan/tasks/main.yml)
- [Delete Image Streamer Golden Image](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Delete_Image_Streamer_Golden_Image/tasks/main.yml)
- [Delete Logical Interconnect](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Delete_Logical_Interconnect_Group/tasks/main.yml)
- [Delete Network Sets](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Delete_Network_Sets/tasks/main.yml)
- [Delete Server Profile](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Delete_Server_Profile/tasks/main.yml)
- [Delete Server Profile Template](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Delete_Server_Profile_Template/tasks/main.yml)
- [Delete Storage Volume](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Delete_Storage_Volume/tasks/main.yml)
- [Delete Storage Volume Template](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Delete_Storage_Volume_Template/tasks/main.yml)
- [Delete User](https://github.com/thopper91/Ansible-HPE_Synergy_Config/blob/master/roles/Delete_User/tasks/main.yml)
