<H1>Andrew Stone Homework Project 1

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

  ![Red Team Diagram](https://github.com/iastoneCO/Diagrams/blob/67767447fd05dd32ea22e2d8d6918bb4750504b8/Img_AndrewStone-RedTeam-Diagram.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the <b>ansible (Yaml)</b> file may be used to install only certain pieces of it, such as Filebeat. -
[Filebeat Config](https://github.com/iastoneCO/HomeWork-Fundamentals-and-Project-13/blob/c6b81f5f1952dbfb12a46632bb4d26142ce25af9/filebeat-config.yml)

 [The Playbook file](https://github.com/iastoneCO/Ansible/blob/838e3c1e147943a9e94decf55c885b72a500e16b/install-elk.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

Load Balancing is the Load balancing is the process of distributing network traffic across multiple servers. By spreading the work evenly, load balancing improves application responsiveness. It also increases availability of applications and websites for users. Modern applications cannot run without load balancers.

What aspect of security do load balancers protect? 
Over time, software load balancers have added additional capabilities including application security.

What is the advantage of a jump box?  A jump box server is a hardened and monitored device that spans two dissimilar security zones and provides a controlled means of access between them.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.

- Filebeat collects data about the file system.
- Metricbeat collects machine metrics, such as uptime.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump-Box-Provisioner | Gateway  | 10.0.0.6   | Linux (Ubuntu)|
| Web-1 (VM1)     |DVWA Container        |10.0.0.4 | Linux (Ubuntu)|
| Web-2 (VM2) | DVWA Container     | 10.0.0.5|Linux (Ubuntu)|
| Web-3 (VM3)|DVWA Container|10.0.0.7    |Linux (Ubuntu)|
| Elk-Server|Elk Server|10.5.0.5 |Linux (Ubuntu)|

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner  machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

Jump-Box:

Machines within the network can only be accessed by Jump-Box (SSH Port 22).

- 104.211.43.19

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box      | No             | 104.211.43.19        |
| Web-1 (VM1)   | No             | 10.0.0.4             |
|  Web-2 (VM2)  | No             | 10.0.0.5             |
|  Web-3 (VM3)  | No             | 10.0.0.7             |
|  Elk-Server   | No             | 40.70.5.58/10.5.0.5  |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Anisble can help you on platform, configuration management, application delopment, intra-service orchestration and provisioning. It is very simply to set and more powerful tool.

The <b>install-elk.yml</b> playbook implements the following tasks:

- Configure Elk VM with Docker
- Install Docker.io
- Install Python pip3
- Download and launch the docker elk container


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

- Web-1 (VM1): 10.0.0.4
- Web-2 (VM2): 10.0.0.5
- Web-3 (VM3): 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat is to transform or enrich your logs and files with Logstash, fiddle with some analystic in Elatisearch, or build and share dashboards in Kibana. 
- Metricbeat collects machine metrics, tracks systems mertic, run CPU and memory usage. 

Filebeat monitors and collects log events on specified servers, then it sends these log files to Kibana

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible.
- Update the /etc/ansible/hosts file to include host group private IP addresses: 
  - 10.0.0.4 ansible_python_interpreter=/usr/bin/python3
  - 10.0.0.5 ansible_python_interpreter=/usr/bin/python3
  - 10.0.0.7 ansible_python_interpreter=/usr/bin/python3

- Run the playbook, and navigate to  http://[Your VM IP Addresses]:5601/app/kibana to check that the installation worked as expected.

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

 how to define “Motd role” and write an ansible playbook to display dynamic Motd on client servers.

- Name: copy the MOTD file over the webserver
  template:
        src: motd.j2
        dest: /etc/motd
  tags:
      -modt_config
