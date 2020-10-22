# ELK-Project
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/Diazultaz/ELK-Project/blob/master/Diagrams/ELK%20Project.png

These files have been tested and used to generate a live ELK deployment on Azure. 
They can be used to either recreate the entire deployment pictured above. 
Alternatively, select portions of the YML playbook file may be used to install only certain pieces of it,
such as Filebeat.

  - elk-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient, in addition to restricting traffic to the network.
- A load balancer will protect against a DDOS attack. The advantage of having a jump box is that admins can connect to a single point for updates and distribute it effectively and efficiently across the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system network.
- Filebeat watches for logs and locations specified, forwards them to the ELK.
- Metricbeat collects data on services running on the server.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address            | Operating System |
|----------|----------|-----------------------|------------------|
| Jump Box | Gateway  | 10.0.0.4 / public IP  | Linux            |
| WEB-1    |   DVWA   | 10.0.0.5              | Linux            |
| WEB-2    |   DVWA   | 10.0.0.6              | Linux            |
| WEB-3    |   DVWA   | 10.0.0.7              | Linux            |
| ELK-VM   |Monitoring| 10.2.0.4 / public IP  | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine and ELK VM can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- IP: 73.204.108.246 "Workstation"
- IP: Virtual network VMs 10.0.0.(5-7)

Machines within the network can only be accessed by workstation via Jump Box.
- ELK VM is accessible via port 5601 via workstation/jumpbox IP: 73.204.108.246

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 73.204.108.246       |
| DVWA VMs | No                  | 10.0.0.4 (JB)        |
| ELK VM   | Yes                 | 73.204.108.246       |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- All task regarding configuration can be done with a few commands from the admin VM, various machines can be configured at a time.

The playbook implements the following tasks:
- The playbook list the ELK host to perform the tasks:
- Installs Docker.io
- Installs Python3
- Installs the Docker module
- Increases the virtual memory to 262144 for ELK to run
- Finally downloads and launch the ELK container.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/Diazultaz/ELK-Project/blob/master/Diagrams/SEBP%20ELK%20761%20CONFIRMED.PNG

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- IP: 10.0.0.5
- IP: 10.0.0.6
- IP: 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat.

These Beats allow us to collect the following information from each machine:

- Will collect information on Syslogs, Sudo commands, SSH logins, and new users and groups.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Copy the install-elk.yml file to etc/ansible directory.
- Update the hosts file to include ELK groups and webservers groups, and target IP address accordingly for ELK and filebeat.
- Run the playbook, and navigate to ELK server and run docker ps to check that the installation worked as expected, also using browser navigation go to http://"fill in ELK public ip address":5601/app/kibana.
