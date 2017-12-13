# Synergy Configuration with Ansible

A group of ansible scripts produced for an account in DXC.technology for OneView in order to configure the HPE Synergy Server

In this Readme file, it states what is required, for a further indepth explanation and a step by step on specific tasks (SDKs etc), please go [to the Wiki](https://github.com/thopper91/Ansible-HPE_Synergy_Config/wiki)

## Required SDKs and tools
Firstly, you will need to install the following:
- OpenSSH
- Ansible
- Python
- Pip
- Unzip
- HP OneView SDK
- HP ICSP
- HP iLO
Once all these have been installed, the environment variables will need to be set to point the Ansible and Python env vars to the new SDK packages

## Playbook, folder and file structure
This information is very important when it comes to working with Ansible. The information can be found here: [Ansible Structure](https://github.com/thopper91/Ansible-HPE_Synergy_Config/wiki/Ansible-Structure---Folder-and-Files)

Something also to take note, Ansible is very 'white-space' sensitive, which means if something is slightly out of line then the playbook will not execute. So to over come this, I used the tool Atom which eliminated that issue but there are others out there also...like Microsoft Visual Studio Code

- [Atom](https://github.com/thopper91/Ansible-HPE_Synergy_Config/wiki/Atom)
- [Microsoft Visual Studio Code](https://github.com/thopper91/Ansible-HPE_Synergy_Config/wiki/Microsoft-Visual-Studio-Code)

I have a set of executable Ansible playbooks here, however that is not the full extent of what I have produced. So if you would like to create a new playbook, its in the same format as these however the role will be different. It will require the role name from the 'roles' folder:
```yml
---
- hosts: all
  connection: local
  roles:
    - {role: NEW_ROLE_NAME}
```

#### Add/Create Playbooks
- [Appliance Time and Locale Configuration](../master/roles/Appliance_Time_and_Locale_Configuration/tasks/main.yml)
- [Attach ISO disk to ILO and server bay](../master/roles/Attach_disk_to_ILO/tasks/main.yml)
- [Create a basic volume disk (100Gb)](../master/roles/Create_Basic_Disk_Template/tasks/main.yml)
- [Create a server profile with ISO attached](../master/roles/Create_Basic_Server_Profile_with_iso_disk_attached/tasks/main.yml)
- [Create a large amount of networks, a mixture of Ethernet and Fibre Channel](../master/roles/Create_Current_Network_Setup/tasks/main.yml)
- [Create a volume disk template for License Cluster](../master/roles/Create_Disk_Template_for_License_Cluster/tasks/main.yml)
- [Create ESXi 6.5 Server Profile with Image Streamer](../master/roles/Create_ESXi_6.5_Profile/tasks/main.yml)
- [Create Enclosure Group](../master/roles/Create_Enclosure_Group/tasks/main.yml)
- [Create Enhanced volume disk template (20Gb)](../master/roles/Create_Enhanced_Disk_Template/tasks/main.yml)
- [Create Ethernet Network](../master/roles/Create_Ethernet_Network/tasks/main.yml)
- [Create Ethernet Network associated to IPv4 subnet](../master/roles/Create_Ethernet_Network_Associated_to_IPv4_Subnet/tasks/main.yml)
- [Create Ethernet network in bulk with same suffix](../master/roles/Create_Ethernet_Network_Bulk_with_same_suffix/tasks/main.yml)
- [Create Fibre Channel Network](../master/roles/Create_Fibre_Channel_Networks/tasks/main.yml)
- [Create Full Enclosure Provision](../master/roles/Create_Full_provision/tasks/main.yml)
- [Create ICsp Server Profile, Server and Deploy OS](../master/roles/Create_ICsp_Profile%2C_Server_and_deploy_OS/tasks/main.yml)
- [Create ICsp Server](../master/roles/Create_ICsp_Server/tasks/main.yml)
- [Create Image Streamer Build Plan](../master/roles/Create_Image_Streamer_Build_Plan/tasks/main.yml)
- [Create Image Streamer Deployment Plan](../master/roles/Create_Image_Streamer_Deployment_Plan/tasks/main.yml)
- [Create Image Streamer Golden Image](../master/roles/Create_Image_Streamer_Golden_Image/tasks/main.yml)
- [Create Image Streamer OpenShift InfraNode Profile](../master/roles/Create_Image_Streamer_OpenShift_InfraNode_Profile/tasks/main.yml)
- [Create Image Streamer OpenShift Master Profile](../master/roles/Create_Image_Streamer_OpenShift_Master_Profile/tasks/main.yml)
- [Create Image Streamer OpenShift Node 1 Profile](../master/roles/Create_Image_Streamer_OpenShift_Node1_Profile/tasks/main.yml)
- [Create Image Streamer OpenShift Node 2 Profile](../master/roles/Create_Image_Streamer_OpenShift_Node2_Profile/tasks/main.yml)
- [Create Image Streamer OpenShift RHEL 7.3 Profile](../master/roles/Create_Image_Streamer_OpenShift_RHEL7.3_Profile/tasks/main.yml)
- [Create IPv4 Ranges](../master/roles/Create_IPv4_Ranges/tasks/main.yml)
- [Create IPv4 Subnet](../master/roles/Create_IPv4_Subnet/tasks/main.yml)
- [Create IPv4 Subnet & Ranges](../master/roles/Create_IPv4_Subnet_%26_Range/tasks/main.yml)
- [Create Logical Enclosure](../master/roles/Create_Logical_Enclosure/tasks/main.yml)
- [Create Logical Interconnect Group](../master/roles/Create_Logical_Interconnect_Group/tasks/main.yml)
- [Create Network Sets](../master/roles/Create_Network_Sets/tasks/main.yml)
- [Create Network Template for Customer VLAN203](../master/roles/Create_Network_Template_for_Customer_VLAN203/tasks/main.yml)
- [Create Network Template for License clusters with Trunked VLANs](../master/roles/Create_Network_Template_for_License_clusters_with_Trunked_VLANs/tasks/main.yml)
- [Create Private Storage Volume](../master/roles/Create_Private_Storage_Volume/tasks/main.yml)
- [Create Profile with Template and Deployment Plan](../master/roles/Create_Profile_with_Template_and_Deployment_Plan/tasks/main.yml)
- [Create SAN Manager](../master/roles/Create_SAN_Manager/tasks/main.yml)
- [Create Server Profile Template](../master/roles/Create_Server_Profile_Template/tasks/main.yml)
- [Create Server Profile from Private SAN](../master/roles/Create_Server_Profile_from_Private_SAN/tasks/main.yml)
- [Create Server Profile via Template](../master/roles/Create_Server_Profile_via_Template/tasks/main.yml)
- [Create Server Profile with Local Storage](../master/roles/Create_Server_Profile_with_Local_Storage/tasks/main.yml)
- [Create Shareable Volume](../master/roles/Create_Shareable_Volume/tasks/main.yml)
- [Create Standard Disk Template](../master/roles/Create_Standard_Disk_Template/tasks/main.yml)
- [Create Storage Systems with Pools](../master/roles/Create_Storage_Systems_with_Pools/tasks/main.yml)
- [Create Storage Volume Template](../master/roles/Create_Storage_Volume_Template/tasks/main.yml)
- [Create User](../master/roles/Create_User/tasks/main.yml)

#### Update Playbooks
- [Update Ethernet Network with Associating a Subnet](../master/roles/Update_Ethernet_Network_with_Associating_a_Subnet/tasks/main.yml)
- [Update Ethernet Network with Removing Subnet](../master/roles/Update_Ethernet_Network_with_Removing_Subnet/tasks/main.yml)
- [Update Profile with SAN](../master/roles/Update_Profile_with_SAN/tasks/main.yml)
- [Update Subnet with new Domain](../master/roles/Update_Subnet_with_new_Domain/tasks/main.yml)
- [Update User Password](../master/roles/Update_User_Password/tasks/main.yml)

#### Gather facts Playbooks
- [Gather Appliance Time and Locale Configuration](../master/roles/Gather_Appliance_Time_and_Locale_Config/tasks/main.yml)
- [Gather Enclosure Facts](../master/roles/Gather_Enclosure_Facts/tasks/main.yml)
- [Gather Enclosure Group URIs](../master/roles/Gather_Enclosure_Group_Uris/tasks/main.yml)
- [Gather Enclosure Groups](../master/roles/Gather_Enclosure_Groups/tasks/main.yml)
- [Gather Ethernet Networks](../master/roles/Gather_Ethernet_Networks/tasks/main.yml)
- [Gather Fibre Channel Networks](../master/roles/Gather_FC_Networks/tasks/main.yml)
- [Gather Firmware Drivers](../master/roles/Gather_Firmware_Drivers/tasks/main.yml)
- [Gather Hardware Facts](../master/roles/Gather_Hardware_Facts/tasks/main.yml)
- [Gather Image Streamer Artifact Bundle](../master/roles/Gather_Image_Streamer_Artifact_Bundle/tasks/main.yml)
- [Gather Image Streamer Build Plans](../master/roles/Gather_Image_Streamer_Build_Plans/tasks/main.yml)
- [Gather Image Streamer Deployment Plan](../master/roles/Gather_Image_Streamer_Deployment_Plan/tasks/main.yml)
- [Gather Image Streamer Golden Image](../master/roles/Gather_Image_Streamer_Golden_Image/tasks/main.yml)
- [Gather Image Streamer OS Volumes](../master/roles/Gather_Image_Streamer_OS_Volumes/tasks/main.yml)
- [Gather Image Streamer Plan Scripts](../master/roles/Gather_Image_Streamer_Plan_Scripts/tasks/main.yml)
- [Gather Logical Interconnect Group](../master/roles/Gather_Logical_Interconnect_Group/tasks/main.yml)
- [Gather Profile Template](../master/roles/Gather_Profile_Template/tasks/main.yml)
- [Gather SAN URIs](../master/roles/Gather_SAN_Uris/tasks/main.yml)
- [Gather SANs](../master/roles/Gather_SANs/tasks/main.yml)
- [Gather Server Profile from Bay](../master/roles/Gather_Server_Profile_from_Bay/tasks/main.yml)
- [Gather Server Profiles](../master/roles/Gather_Server_Profiles/tasks/main.yml)
- [Gather Storage Pools](../master/roles/Gather_Storage_Pools/tasks/main.yml)
- [Gather Users](../master/roles/Gather_Users/tasks/main.yml)
- [Gather Volume Template](../master/roles/Gather_Volume_Template/tasks/main.yml)
- [Gather Volumes](../master/roles/Gather_Volumes/tasks/main.yml)
- [Gather ALL Network URIs](../master/roles/Gather_all_Network_Uris/tasks/main.yml)

#### Other Playbooks
- [Download Artifact Bundle](../master/roles/Download_Artifact_Bundles/tasks/main.yml)
- [Download and use SPP file](../master/roles/Download_and_upload_SPP/tasks/main.yml)
- [Ensure IPv4 Range is Disabled](../master/roles/Ensure_IPv4_Range_is_Disabled/tasks/main.yml)
- [Ensure IPv4 Range is Enabled](../master/roles/Ensure_IPv4_Range_is_Enabled/tasks/main.yml)
- [ICsp OS Deployment](../master/roles/ICsp_OS_Deployment/tasks/main.yml)
- [Image Streamer Artifact Bundle Download and Upload](../master/roles/Image_Streamer_Artifact_Bundle_Download_%26_Upload/tasks/main.yml)
- [Image Streamer Upload & Extract Artifact Bundle](../master/roles/Image_Streamer_Upload_%26_Extract_Artifact_Bundle/tasks/main.yml)
- [Momentary Press Power Off Server](../master/roles/Momentory_Press_Power_Off_Server/tasks/main.yml)
- [Momentary Press Power On Server](../master/roles/Momentory_Press_Power_On_Server/tasks/main.yml)
- [Press and Hold Power Off Server](../master/roles/Press_and_Hold_Power_Off_Server/tasks/main.yml)

#### Delete Playbooks
- [Delete Enclosure Groups](../master/roles/Delete_Enclosure_Groups/tasks/main.yml)
- [Delete Ethernet Network](../master/roles/Delete_Ethernet_Network/tasks/main.yml)
- [Delete Fibre Channel Network](../master/roles/Delete_Fibre_Channel_Network/tasks/main.yml)
- [Delete IPv4 Range](../master/roles/Delete_IPv4_Range/tasks/main.yml)
- [Delete IPv4 Subnet](../master/roles/Delete_IPv4_Subnet/tasks/main.yml)
- [Delete IPv4 Subnet & Range](../master/roles/Delete_IPv4_Subnet_%26_Range/tasks/main.yml)
- [Delete Image Streamer Artifact Bundle](../master/roles/Delete_Image_Streamer_Artifact_Bundle/tasks/main.yml)
- [Delete Image Streamer Build Plan](../master/roles/Delete_Image_Streamer_Build_Plan/tasks/main.yml)
- [Delete Image Streamer Deployment Plan](../master/roles/Delete_Image_Streamer_Deployment_Plan/tasks/main.yml)
- [Delete Image Streamer Golden Image](../master/roles/Delete_Image_Streamer_Golden_Image/tasks/main.yml)
- [Delete Logical Interconnect](../master/roles/Delete_Logical_Interconnect_Group/tasks/main.yml)
- [Delete Network Sets](../master/roles/Delete_Network_Sets/tasks/main.yml)
- [Delete Server Profile](../master/roles/Delete_Server_Profile/tasks/main.yml)
- [Delete Server Profile Template](../master/roles/Delete_Server_Profile_Template/tasks/main.yml)
- [Delete Storage Volume](../master/roles/Delete_Storage_Volume/tasks/main.yml)
- [Delete Storage Volume Template](../master/roles/Delete_Storage_Volume_Template/tasks/main.yml)
- [Delete User](../master/roles/Delete_User/tasks/main.yml)
