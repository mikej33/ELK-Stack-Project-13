## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Azure Cloud
![Update the path with the name of your diagram](Images/Azure_CloudSecurity.PNG)
Azure Cloud with Elk Stack
![Update the path with the name of your diagram](Images/Azure_CloudSecurity_ELK.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the __playbook__ file may be used to install only certain pieces of it, such as Filebeat.

  - __Host,Ansible.cfg,my_playbook.yml,filebeat-config.yml,filebeat-playbook.yml,install-elk.yml,metricbeat-config.yml__

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly __Available__, in addition to restricting __access__ to the network.

-What aspect of security do load balancers protect? What is the advantage of a jump box?
__Load Balancers protect the network from Distribute denial-of-Server attacks (DDoS) by shifting the attack traffic from corporate server back to cloud provider. Jumpbox seperates or allow the WebVms to be in a seperate security zone which protects the WebVMs from public access and potential security breach__

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the __Server logs__ and system __metrics__.
- What does Filebeat watch for?   __Filebeats monitor the log files or locations you specify__

- What does Metricbeat record? __It records metric data from target Servers such as OS metrics, memory, other beats, and metrics you specify__


The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Ansible  | 10.1.0.6   | Linux            |
| Elk      | Elkstack | 10.3.0.5   | Linux            |
| Web-1    |  Docker  | 10.1.0.4   | Linux            |
| Web-2    |  Docker  | 10.1.0.5   | Linux            |
| Web-3    |  Docker  | 10.1.0.13  | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the __gateway__ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- __107.205.7.103 (My Home IP address)__

Machines within the network can only be accessed by __using SSH connection__.
- Which machine did you allow to access your ELK VM? What was its IP address?  __10.1.0.6_

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 107.205.7.103        |
|  Elk     | Yes                 | 107.205.7.103        |
|  Web-1   | No                  | 10.3.0.5, 10.1.0.6   |
|  Web-2   | No                  | 10.3.0.5, 10.1.0.6   |
|  Web-3   | No                  | 10.3.0.5, 10.1.0.6   |
|  LB      | Yes                 | 107.205.7.103        |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible? 
- __Using Ansible save a lot of time that is saved instead of manually installing the software. Ansible has a big costing in that it is virtual install rather than buying expense hardware. Ansible allows for easy configuration and setup and maintenance__
  _

The playbook implements the following tasks:
In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc.
- Create a new Vnet
- Create a Peer Network Connection
- Edit Ansible cfg on Jumpbox
- Create ELK playbook
- Download Docker container 
- Install and configured the ELK container..

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Update the path with the name of your screeshot of your docker](Images/Docker_ps_output.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- __10.1.0.4, 10.1.0.5,10.1.0.13__  

We have installed the following Beats on these machines:
- __I successfully installed Filebeat and Metricbeat__

These Beats allow us to collect the following information from each machine:
In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
- __Filebeats monitor the log files, or locations you specify. One log i monitor was the IIS logs. Expect to see Response codes overtime or Error logs overtime__. 
- __Metricbeat records metric data from target Servers such as OS metrics, memory, other beats, and metrics you specify. I montiored the CPU and Memory Usage__


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the __YAML__ file to __Ansible_ __VM___.
- Update the __YAML_ __Playbook___ file to include App Install, Virtual Memory increase, Download and launc docker elk
- Run the playbook, and navigate to __home and run sudo docker ps__ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- Which file is the playbook? __install-elk.yml__
- Where do you copy it?   __ansible of jump box to home/etc/ansible__
- Which file do you update to make Ansible run the playbook on a specific machine? __hosts__
- How do I specify which machine to install the ELK server on versus which to install Filebeat on? __comment the host file with [elk], then include the server IP address and version of python to run__


- Which URL do you navigate to in order to check that the ELK server is running? __http://20.119.192.185:5601/app/kibana__

- As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc. __ansible-playbook install-elk.yml__
