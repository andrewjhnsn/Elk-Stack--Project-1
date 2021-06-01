Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.
  



These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Playbook File may be used to install only certain pieces of it, such as Filebeat.
* Filebeats-playbook.yml
* Install-Elk-Playbook.yml
* Metricbeat-Playbook.yml
*  My-Playbook.yml
* Hosts File
* Metricbeat-config.yml
* Filebeat-config.yml
This document contains the following details:
* Description of the Topology
* Access Policies
* ELK Configuration
   *   Beats in Use
   *   Machines Being Monitored
* How to Use the Ansible Build


Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly available, in addition to restricting access to the network. Load Balancers help ensure the network availability by the distributing of the data that incoming to the web servers. 
Jump-Box-Provisioner allows easy access and management of multiple macjones. It also allows for multiple machines to be added when necessary without recreating a whole new network structure. It provides an extra layer of protection to your system. 
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the events logs and system metrics.
* Filebeat watches for log files/locations and collects log events.
* Metricbeat helps you monitor your servers by collecting metrics from the system and services running on the server.


The configuration details of each machine may be found below.
Name                            Function                   IP Address           Operating System 
Jump Box                      Gateway                    10.0.0.4                     Linux            
 Web-1                     WebServer            10.0.0.5                     Linux            
 Web-2                            WebServer             10.0.0.6                    Linux            
 Django-vm1          Log Server          10.1.0.5                     Linux            
 


Access Policies
The machines on the internal network are not exposed to the public Internet.
Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
Personal IP Address
Machines within the network can only be accessed by Jump-Box-Provisioner.
* The Django-vm1 is only accessible by SSH from the JumpBox and internet access from Personal IP Address through port 5601


A summary of the access policies in place can be found in the table below.


 Name                 Publicly Accessible          Allowed IP Addresses
Jump-Box                 No                                   Workstation Public IP on SSH 22 
Load Balancer                 No                                Workstation Public IP on HTTP 80
Web-1                        No                                10.0.0.5 on SSH 22
Web-2                        No                                10.0.0.6 on SSH 22
Django-vm1                No                                Workstation Public IP on TCP 5601                                                                        










 Elk Configuration


Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
* The main advantage of automating the configuration of the Django-vm1(Elk Server) helped the process of being able to create and install  multiple servers. Which makes it easy to deploy them without having to physically touch each server.




The playbook implements the following tasks:
1. Install Docker.io and pipaDownload and Configure elk docker container
2. Increases VM memory
3. Install Docker.io and pip3
4. Sets Published Ports




The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.  


![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)




Target Machines & Beats
This ELK server is configured to monitor the following machines:
* Web-1 10.0.0.5
* Web-2 10.0.0.6


We have installed the following Beats on these machines:
* Filebeat
* Metricbeat


These Beats allow us to collect the following information from each machine:
* Filebeat watches for log files/locations and collects log events. Winlogbeat, for example, ships Windows event logs. 
* Metricbeat helps you monitor your servers by collecting metrics from the system and services running on the server. For example, you can use Metricbeat to monitor and analyze system CPU, memory and load. 


Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:


SSH into the control node and follow the steps below:
* Copy the Elk Installation and VM Configuration through Ansible.
* Run the command ansible-playbook Install-Elk-Playbook.yml. This will activate the playbook 
* Verifying the playbook is active. You can run the command of ansible-playbook Install-Elk-Playbook.yml again and all status should be say ok in a green color.   
* Run the playbook, and navigate to Django-vm1(PublicIP:5601/app/kibana) to check that the installation worked as expected.




Which file is the playbook? Where do you copy them?
* The Playbook is a .yml file. You copy the file to the source and destination that you want the file to be located. 
Which file do you update to make Ansible run the playbook on a specific machine?
* /etc/ansible/host
 How do I specify which machine to install the ELK server on versus which to install Filebeat on?
* Update the Host file, to specify you add the private IP under elk and not web servers in the hosts file..


Which URL do you navigate to in order to check that the ELK server is running?
* http://(PublicIP:5601/app/kibana)


Specific commands the user will need to run to download the    playbook
* sudo apt-get update
* sudo apt install docker.io
* sudo service docker start
* systemctl status docker
* sudo docker pull cyberxsecurity/ansible
* sudo docker run -ti cyberxsecurity/ansible bash
* sudo docker start
* sudo docker ps -a
* sudo docker ps -a
* Ssh-keygen
* ansible -m ping all
* Ansible-playbook (playbook name)