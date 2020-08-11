# Elk-Stack-Project-

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/Elk Stack Project.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._
---
- name: Installing and Launch Filebeat
  hosts: webservers
  become: yes
  tasks:
    # Use command module
  - name: Download filebeat .deb file
    command: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.4$
    # Use command module
  - name: Install filebeat .deb
    command: dpkg -i filebeat-7.4.0-amd64.deb
    # Use copy module
  - name: Drop in filebeat.yml
    copy:
      src: /etc/ansible/files/filebeat-config.yml
      dest: /etc/filebeat/filebeat.yml
    # Use command module
  - name: Enable and Configure System Module
    command: filebeat modules enable system

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficent, in addition to restricting access to the network.
- What aspect of security do load balancers protect? What is the advantage of a jump box? Loadbalancers create an extra layer of protection for your server by Protect applications from emerging threats, The load balancer can request a username and password before granting access to your website to protect against unauthorized access, also can detect and drop distributed denial-of-service (DDoS) traffic before it gets to your website. The main benefits of JumpBox are its extensive software library, automated backups, and customizations. Resources can be focused on more critical activities once open-source apps are run as JumpBoxes. This also allows users to run their apps wherever they may be.Users also don’t have to worry about spending long amounts of time running application evaluations. JumpBox also makes it possible for users to immediately use the apps, even before the hardware they need is present. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log data and system metrics.
- What does Filebeat watch for?_Filebeat consists of two main components: inputs and harvesters. These components work together to tail files and send event data to the output that you specify. A harvester is responsible for reading the content of a single file. An input is responsible for managing the harvesters and finding all sources to read from. 
- What does Metricbeat record?_Metricbeat collects a variety of metrics from your server (i.e. operating system and services) and ships them to an output destination of your choice.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function  | IP Address | Operating System |
|----------|---------- |------------|------------------|
| Jump Box | Gateway   | 10.0.0.1   | Linux            |
| ELK Serve| Monitoring| 10.1.0.4   | Linux            |
| Web - 1  | VM        | 10.0.0.5   | Linux            |
| Web - 2  | Redundancy| 10.0.0.6   | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 24.28.107.86 Home Network 

Machines within the network can only be accessed by Secure Shell.
- Which machine did you allow to access your ELK VM? What was its IP address? A Secureshell by the Jumpbox - 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 |  24.28.107.86        |
| Web - 1  | NO                  |  10.1.0.4            |
| Web - 2  | NO                  |  10.1.0.4            |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because this would allow other networks to be built in the same way, and make the task of building them alot easier. 

The playbook implements the following tasks:
- Install Docker.io
- Install pip3
- Install Docker python module
- Increase Virtual Memory
- Download and launch a Docker Elk Container 


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web 1: 52.142.3.108 
- Web 2: 52.142.3.108

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat  

These Beats allow us to collect the following information from each machine:
- Filebeat - Log files, locationsm and events. 
- Metricbeat - system metrics and services running.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible.
- Update the /etc/ansible/hosts file to include the [elk] group and the VM under the elk group.
- Run the playbook, and navigate to the load balancer (52.142.3.108 (RedteamLB-RFJ)) to check that the installation worked as expected.

- Reference this file and place into the /etc/ansible directory
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running? 

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
