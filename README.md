# _Unit_13_Elk_Project_

The files in this repository were used to configure the network depicted below:

![ELK Project Diagram drawio (1)](https://user-images.githubusercontent.com/85268980/141315392-3d31aa40-91cd-4d75-8a48-18baf49929d1.png)

These have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the playbook (yml) file may be used to install only certain pieces of it, such as Filebeat.

The following is an example of an installation YAML file used in this project:

![ELK-Install YML File](https://user-images.githubusercontent.com/85268980/141399444-a09e6100-7e45-4bc1-9488-731c7ef3c009.png)


The following sections of this document contains:

       -A Description of the Topology
   
       -Access Policies
   
       -ELK Configuration 
       
       -Target Machines and Beats
  
       -How to Use the Ansible Build

_**A Description of the Topology**_

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


|   Name  |  Function | IP Address |Operating System/ Version|            Size of Machine           |   Exposed Ports    | Allowed IP Addresses    |
|:-------:|:---------:|:----------:|:-----------------------:|:------------------------------------:|:------------------:|:-----------------------:|
| JumpBox |  Gateway  |  10.0.0.4  |  Linux (Ubuntu 18.04)   | Standard B1s (1 vcpus, 1 GiB memory) |     22, 80         |Local Desktop IP Address|
|  Web-1  | Webserver |  10.0.0.7  |  Linux (Ubuntu 18.04)   | Standard B1ms (1 vcpus, 2 GiB memory)|     22, 80         |Load Balancer Public IP: 13.82.23.122/ JumpBox IP: 10.0.0.4|
|  Web-2  | Webserver |  10.0.0.9  |  Linux (Ubuntu 18.04)   | Standard B1ms (1 vcpus, 2 GiB memory)|     22, 80         |Load Balancer Public IP: 13.82.23.122/ JumpBox IP: 10.0.0.4|
|  Web-3  | Webserver |  10.0.0.8  |  Linux (Ubuntu 18.04)   | Standard B1ms (1 vcpus, 2 GiB memory)|     22, 80         |Load Balancer Public IP: 13.82.23.122/ JumpBox IP: 10.0.0.4||  
Elk-VM | Webserver |  10.1.0.4  |  Linux (Ubuntu 18.04)   | Standard B2s (2 vcpus, 4 GiB memory) | 22, 80, 5601, 9200 |Load Balancer Public IP: 13.82.23.122/ JumpBox IP: 10.0.0.4|


_**Access Policies**_

The machines on the internal network are not exposed to the public Internet. Only the JumpBox Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

    A: Local Desktop IP
    
Machines within the network can only be accessed by JumpBox Provisioner.

The Elk-VM is only accessbile via SSH from the Jump Box through web access from the Host IP address. A summary of the access policies in place can be found in the table below:


   |   Name  | Publicly Accessible |                      Allowed IP Address                   |
   |:-------:|:-------------------:|:---------------------------------------------------------:|
   | JumpBox |          Yes        |            Local Desktop IP: 184.96.185.20                |
   |  Web-1  |          No         |   Private IP: 10.0.0.4/ Load Balancer IP: 13.82.23.122    |
   |  Web-2  |          No         |   Private IP: 10.0.0.4/ Load Balancer IP: 13.82.23.122    |
   |  Web-3  |          No         |   Private IP: 10.0.0.4/ Load Balancer IP: 13.82.23.122    |
   |  Elk-VM |          No         |   Private IP: 10.0.0.4/ Load Balancer IP: 13.82.23.122    |


_**Elk Configuration**_

Using the command above, Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because of...

    A: -The ability to deploy multiple servers easily without touching each server.
       -Increased efficiency due to not having to install additional virtual machines which can be bulky and wasteful of memory.
       -Ansible being able to allow models of highly complex workflows in IT.

The playbook implements the following tasks:
   -Install Docker
   -Install Elasticsearch
   -Install Logstash
   -Install Kibana
   -Install Beats

The following screenshot displays the result of running the 'sudo docker ps' command after successfully configuring the ELK instance.

![Screen Shot 2021-11-10 at 7 28 53 PM](https://user-images.githubusercontent.com/85268980/141226735-ca402d75-7df9-4db2-8129-cc0c0d6b606f.png)

_**Target Machines & Beats**_

This ELK server is configured to monitor the following machines:

| Name  | IP Address |
|:-----:|:----------:|
| Web-1 |  10.0.0.7  |
| Web-2 |  10.0.0.9  |
| Web-3 |  10.0.0.8  |
| Elk-VM |  10.1.0.4  |

We have installed the following Beats on these machines:

    -Filebeat
    -Metricbeat

These Beats allow us to collect the following information from each machine:

    -Filebeat monitors for log files and locations and collects log activities.(Filebeat: Lightweight Log Analysis & Elasticsearch)
    
    The following is an example of a Filebeat command:
    
   ![Filebeat YML file](https://user-images.githubusercontent.com/85268980/141225132-78e6f466-82b8-4edb-9233-d7f7196db25b.png)

    -Metricbeat records metrics and statistical data from the operating system and from services running on the server.(Metricbeat: Lightweight Shipper for Metrics)
    
    The following is an example of a Metricbeat command:
    
   ![Metricbeat YML File](https://user-images.githubusercontent.com/85268980/141225068-a5e93d78-940b-47cb-b9d3-6f9d3b128822.png)
    
_**Using the Playbook**_

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:
SSH into the control node and follow the steps below:

      - Copy the ssh-keygen file to ssh public key.
      - Update the security rule file to include the IP address.
      - Run the playbook, and navigate to http://40.78.91.91:5601/app/kibana to check that the installation worked as expected.

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

In this scenario, the URL you will verify the ELK server is at __http://40.78.91.91:5601/__ and should look like the following displayed below:

![Kibana Working](https://user-images.githubusercontent.com/85268980/138544651-9c893be3-80e1-49da-aa3a-663a2a7b3592.png)
