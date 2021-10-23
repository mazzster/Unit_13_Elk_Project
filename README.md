# Unit_13_Elk_Project

The files in this repository were used to configure the network depicted below:

![Screen Shot 2021-10-22 at 11 25 22 PM](https://user-images.githubusercontent.com/85268980/138543676-8c9b61a5-cbe6-4c1f-919c-ac3d2cdcce1d.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _playbook (yml) file_ may be used to install only certain pieces of it, such as Filebeat.

_install_elk.yml_

This document contains the following details:

       -Description of the Topology
   
       -Access Policies
   
       -ELK Configuration (Beats in Use Machines Being Monitored)
  
       -How to Use the Ansible Build


**Description of the Topology**
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

    Q: What aspect of security do load balancers protect? 
    A: - Load balancers work to protect an organiztion's servers from incoming malicious traffic.
       - Several examples of malicious attacks include daily rule updates, username and password requests and verification, as well as DDOS attacks that can overwhelm servers.
       

    Q: What is the advantage of a jump box?
    A: -This can act as a single entry point for a user to gain access.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.

    Q: What does Filebeat watch for?
    A: - Filebeat monitors log files or specified locations, collects log events, and also forwards them for indexing based on the configured settings.
    

    Q: What does Metricbeat record?
    A: -Metricbeat will periodically collect metrics from OS or any services that run on a server, it then ships these metrics to any output that is tied to the configuration.

The configuration details of each machine may be found below:


|   Name  |  Function | IP Address | Operating System |
|:-------:|:---------:|:----------:|:----------------:|
| JumpBox |  Gateway  |  10.0.0.4  |       Linux      |
|  Web-1  | Webserver |  10.0.0.7  |       Linux      |
|  Web-2  | Webserver |  10.0.0.9  |       Linux      |
|  Elk-VM | Webserver |  10.1.0.4  |       Linux      |


**Access Policies**
The machines on the internal network are not exposed to the public Internet.
Only the JumpBox Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

A: 5601 Kibana Port

Machines within the network can only be accessed by JumpBox Provisioner.

Q: Which machine did you allow to access your ELK VM? What was its IP address?
A: The Elk-VM is only accessbile via SSH from the Jump Box through web access from the Host IP address.

A summary of the access policies in place can be found in the table below:


|   Name  | Publicly Accessible | Allowed IP Address |
|:-------:|:-------------------:|:------------------:|
| JumpBox |         Yes         |   Host IP Address  |
|  Web-1  |          No         |      10.0.0.4      |
|  Web-2  |          No         |      10.0.0.4      |
|  Elk-VM |          No         |      10.0.0.4      |


**Elk Configuration**
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
A: -Ability to delpoy multiple servers easily without touching each server
   -Efficiency due to not having to install additional virtual machines which can be bulky and waste ful of memory
   -Ansible is able to allow models of highly complex workflows in IT.

The playbook implements the following tasks:
   -Install Docker
   -Install Elasticsearch
   -Install Logstash
   -Install Kibana
   -Install Beats

The following screenshot displays the result of running sudo docker ps after successfully configuring the ELK instance.

![Sudo Docker Ps](https://user-images.githubusercontent.com/85268980/138542891-7752fbe1-174b-4618-94fa-10bcc1200cf7.png)

**Target Machines & Beats**
This ELK server is configured to monitor the following machines:

|  Name | IP Address |
|:-----:|:----------:|
| Web-1 |  10.0.0.7  |
| Web-2 |  10.0.0.9  |

We have installed the following Beats on these machines:

      Filebeat
      Metricbeat

These Beats allow us to collect the following information from each machine:

    - Filebeat monitors for log files and locations and collects log activities.(Filebeat: Lightweight Log Analysis & Elasticsearch)

    -Metricbeat records metrics and statistical data from the operating system and from services running on the server.(Metricbeat: Lightweight Shipper for Metrics)
    
    _metricbeat-playbook.yml_

**Using the Playbook**

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:
SSH into the control node and follow the steps below:

      - Copy the ssh-keygen file to ssh public key.
      - Update the security rule file to include the IP address.
      - Run the playbook, and navigate to http://40.78.91.91:5601/app/kibana to check that the installation worked as         expected.

Which file is the playbook? Where do you copy it?


Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?

      $ cd /etc/ansible
      $ cat > hosts <<EOF
      [webservers]
      10.0.0.7
      10.0.0.9 
      
      [elk]
      10.1.0.4
      EOF

The URL you will verify the ELK server is at __http://(ELK-VMpublicIP):5601/__

![Kibana Working](https://user-images.githubusercontent.com/85268980/138544651-9c893be3-80e1-49da-aa3a-663a2a7b3592.png)
