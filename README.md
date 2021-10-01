## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![network diagram](Images/Network_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above or, alternatively, select portions of the .yml playbook files may be used to install only certain pieces of it, such as Filebeat.

The following Ansible playbooks were used to install DVWA and the ELK stack:

  - install-DVWA.yml
  - install-elk.yml
  - filebeat-playbook.yml
  - metricbeat-playbook.yml

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
- The aspect of security that load balancers protect is availability, one of the three security aspects of the CIA Triad. The use of a load balancer mitigates denial of service attacks by distributing to web traffic among the web servers in the backend pool.

- The advantage of using a jump box in the virtual network is that it provides access to the network for centralized administration. It can be locked down so that only those authorized administrators have access. One disadvantage is that it can become tedious to maintain NSG rules if there are a lot of changes to network administrator personnell. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.

- Filebeat monitors log files, collects log events, and forwards them to Elasticsearch or Logstash.
- Metricbeat records metrics from the operating system and from services running on the server.

The configuration details of each machine may be found below.

|       Name       |  Function  |                 IP Address                 | Operating System |
|:----------------:|:----------:|:------------------------------------------:|:----------------:|
| RedTeam-jumphost |   Gateway  | 10.0.0.4 (Private) 52.191.114.223 (Public) |      Ubuntu      |
|   RedTeam-web1   | Web Server |                  10.0.0.5                  |      Ubuntu      |
|   RedTeam-web2   | Web Server |                  10.0.0.6                  |      Ubuntu      |
|   RedTeam-web3   | Web Server |                  10.0.0.7                  |      Ubuntu      |
|        ELK       | ELK Server | 104.42.159.110 (Public) 10.1.0.5 (Private) |      Ubuntu      |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the RedTeam-jumphost machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Personal IP Address

Machines within the network can only be accessed by SSH.
- The ELK VM can be accessed via SSH from the RedTeam-jumphost and via HTTP (port 80) from a personal IP address.

A summary of the access policies in place can be found in the table below.

| Name             | Publicly Accessible    | Allowed IP Addresses                                                                 |
|------------------|------------------------|--------------------------------------------------------------------------------------|
| RedTeam-jumphost | No                     | Personal IP Address                                                                  |
| RedTeam-web1     | Yes, via load balancer | 20.85.226.54                                                                         |
| RedTeam-web2     | Yes, via load balancer | 20.85.226.54                                                                         |
| RedTeam-web3     | Yes, via load balancer | 20.85.226.54                                                                         |
| ELK              | No.                    | SSH from RedTeam-jumphost (10.0.0.4) and  HTTP from personal IP address on port 5601 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- the main advantage of automating configuration with Ansible is that configurations are consistent. Once the playbook files have been created and tested,
  they can be used to configure as many systems as required and they will all be the same.

The playbook implements the following tasks:
- installs docker.io, pip3, and the docker python module
- increases virtual memory required to run the ELK stack
- downloads and launches the docker elk container
- sets restart policy
- maps the required ports

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

!(Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

- RedTeam-web1 (10.0.0.5)
- RedTeam-web2 (10.0.0.6)
- RedTeam-web3 (10.0.0.7)

We have installed the following Beats on these machines:

- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?