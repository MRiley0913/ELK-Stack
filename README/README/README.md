## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

See Images folder

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

  - filebeat-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly secure, in addition to restricting unauthorized access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the servers and system logs.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name      | Function | IP Address | Operating System |
|-----------|----------|------------|------------------|
| Jump Box  | Gateway  | 10.0.0.4   | Linux            |
| Web-1     | DVWA     | 10.0.0.5   | Linux            |
| Web-2     | DVWA     | 10.0.0.6   | Linux            |
| Web-3     | DVWA     | 10.0.0.7   | Linux            |
| ELK-Stack | ELK      | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 13.90.41.137

Machines within the network can only be accessed by the Jump Box
- 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses               |
|-----------|---------------------|------------------------------------|
| Jump Box  | No                  | 24.198.198.212                     |
| Web-1     | No                  | 10.0.0.4  10.1.0.4  24.198.198.212 |
| Web-2     | No                  | 10.0.0.4  10.1.0.4  24.198.198.212 |
| Web-3     | No                  | 10.0.0.4  10.1.0.4  24.198.198.212 |
| ELK-Stack | Yes                 | 10.0.0.4  24.198.198.212           |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because using playbooks you can 
deploy multiple machines at once with minimal effort and it ensures that all machines are indentical without the chance of human error

The playbook implements the following tasks:
- Downloads the Filebeat & Metricbeat deb files
- Installs the downloaded files
- Copies filebeat.yml and metricbeat.yml to appropriate destinations
- Enables and configures the system modules
- Sets up Filebeat & Metricbeat
- Starts Filebeat and Metricbeat services

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

See Images folder

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5 10.0.0.6 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects logs and packages them to send to logstash
- Metricbeat takes the metrics and statistics that it collects and ships them to the output that ypu choose

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the configuration file to /etc/filebeat/filebeat.yml
- Update the config file to include the elk VM and the web VM's IP addresses and be sure to add them to the hosts file as well
- Run the playbook, and navigate to [load balancer IP]/setup.php to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it? filebeat-playbook.yml is the file and you copy it to /etc/ansible/roles
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? You updates the hosts file to designate which IP belobg to which machine
- _Which URL do you navigate to in order to check that the ELK server is running? [local machine IP]:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.
To download the configuration file, run curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/files/filebeat-config.yml
To configure this file to your system you will need to then use "nano" to edit the downloaded file
To update the host file you will need to navigate to it under etc/ansible and edit it using "nano hosts"
To run the playbook once you have downloaded it you simply connect to your ansible container and run the command: ansible-playbook filebeat-playbook.yml