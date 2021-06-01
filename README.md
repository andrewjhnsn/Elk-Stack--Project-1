## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
![image](https://user-images.githubusercontent.com/74883969/120398363-125a6200-c308-11eb-8d19-83a7b4e13206.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Playbook file may be used to install only certain pieces of it, such as Filebeat.

  -  [my-playbook](https://github.com/andrewjhnsn/Elk-Stack-Project-1/blob/main/Ansible/yml-Playbooks/my-playbook.yml)- 
- [install-elk-playbook.yml](https://github.com/andrewjhnsn/Elk-Stack-Project-1/blob/main/Ansible/yml-Playbooks/install-elk-playbook.yml)

-	[filebeats-playbook.yml](https://github.com/andrewjhnsn/Elk-Stack-Project-1/blob/main/Ansible/yml-Playbooks/filebeats-playbook.yml)

-	[metricbeats-playbook.yml](https://github.com/andrewjhnsn/Elk-Stack-Project-1/blob/main/Ansible/yml-Playbooks/metricbeats.playbook.yml)

-	[Filebeat-config.yml](https://github.com/andrewjhnsn/Elk-Stack-Project-1/blob/main/Ansible/yml-Playbooks/Filebeat-config.yml)
-	[Metricbeats-config.yml](https://github.com/andrewjhnsn/Elk-Stack-Project-1/blob/main/Ansible/yml-Playbooks/Metricbeat.config.yml)
-	[Hosts-File](https://github.com/andrewjhnsn/Elk-Stack-Project-1/blob/main/Ansible/yml-Playbooks/Hosts%20File)


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

-Jump-Box-Provisioner allows easy access and management of multiple macjones. It also allows for multiple machines to be added when necessary without recreating a whole new network structure. It provides an extra layer of protection to your system.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the event logs and system system metrics.
- Filebeat- watches for log files/locations and collects log events.

- Metricbeat- helps you monitor your servers by collecting metrics from the system and services running on the server.



The configuration details of each machine may be found below.
 | Name                    | Function  | IP Address  | Operating System |
 |-------------------------|-----------|-------------|------------------|
 | Jump Box                | Gateway   | 10.0.0.4    | Linux            |
 | Web-1                   | Webserver | 10.0.0.5    | Linux            |
 | Web-2                   | Webserver | 10.0.0.6    | Linux            |
 | Django-vm1 (Elk Server) | Log Sever | 10.1.0.5    | Linux            |



### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Personal IP Address

Machines within the network can only be accessed by Jump-Box-Provisioner.
- The Django-vm1(Elk Server) is only accessible by SSH from the Jump-Box and internet access from Personal IP Address through port 5601

A summary of the access policies in place can be found in the table below.
| Name                    | Publicly Accessible | Allowed IP Addresses              |
|-------------------------|---------------------|-----------------------------------|
| Jump Box                | No                  | Workstation Public IP on SSH 22   |
| Web-1                   | No                  | 10.0.0.5 on SSH 22                |
| Web-2                   | No                  | 10.0.0.6 on SSH 22                |
| Load Balancer           | No                  | Workstation Public IP on HTTP 80  |
| Django-vm1 (Elk Server) | No                  | Workstation Public IP on TCP 5601 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The main advantage of automating the configuration of the Django-vm1(Elk Server) helped the process of being able to create and install multiple servers. Which makes it easy to deploy them without having to physically touch each server.

-[Install-ElK-Playbook](https://github.com/andrewjhnsn/Elk-Stack-Project-1/blob/main/Ansible/yml-Playbooks/install-elk-playbook.yml)implements the following tasks:
- Download and Configure elk docker container 
- ---
     - name: Configure Elk VM with Docker
       hosts: elk
       remote_user: redadmin
       become: true
       tasks:

- Increases virtual memory

  - name: Increase virtual memory
     command: sysctl -w vm.max_map_count=262144

   - name: Use more memory
     sysctl:
       name: vm.max_map_count
       value: '262144'
       state: present
       reload: yes

-Install Docker.io and pip3
- name: Install docker.io
     apt:
       update_cache: yes
       force_apt_get: yes
       name: docker.io
       state: present
       
   - name: Install python3-pip
     apt:
       force_apt_get: yes
       name: python3-pip
       state: present

-Download the Docker Elk Container - name: download and launch a docker elk container
     docker_container:
       name: elk
       image: sebp/elk:761
       state: started
       restart_policy: always
       published_ports:
         -  5601:5601
         -  9200:9200
         -  5044:5044

-Make sure Docker is enable to start on reboot
- name: Enable service docker on boot
     systemd:
       name: docker
       enabled: yes




The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
 
!

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
  - Web-1 10.0.0.5
- Web-2 10.0.0.6


We have installed the following Beats on these machines:
•	- Filebeat
•	-Metricbeat


These Beats allow us to collect the following information from each machine:
-  Filebeat watches for log files/locations and collects log events. Winlogbeat, for example, ships Windows event logs
- Metricbeat helps you monitor your servers by collecting metrics from the system and services running on the server. For example, you can use Metricbeat to monitor and analyze system CPU, memory and load.	

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Elk Installation and VM Configuration through Ansible..
- Run the command ansible-playbook Install-Elk-Playbook.yml. This will activate the playbook
- Verifying the playbook is active. You can run the command of ansible-playbook Install-Elk-Playbook.yml again and all status should be say ok in a green color.
- Run the playbook, and navigate to Django-vm1(PublicIP:5601/app/kibana) to check that the installation worked as expected.


##Which file is the playbook? Where do you copy it?_
- Which file do you update to make Ansible run the playbook on a specific machine?
•	 -Answer: /etc/ansible/host
 
-How do I specify which machine to install the ELK server on versus which to install Filebeat on?_

-Answer: Update the Host file, to specify you add the private IP under elk and not web servers in the hosts file.

- _Which URL do you navigate to in order to check that the ELK server is running?
-Answer: http://(PublicIP:5601/app/kibana)



