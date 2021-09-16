## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Images/ELK-VNET-Diagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml file may be used to install only certain pieces of it, such as Filebeat.

  - /etc/ansible/install-elk.yml
  - /etc/ansible/filebeat-playbook.yml
  - /etc/ansible/metricbeat-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _____, in addition to restricting access to the network.
- Load balancers ensures that a website's server is never overloaded by rerouting which client goes to which website's server. In turn if a server is down, the load balancer can reroute those to the other server preventing any sort of Denia of Service attack.
- A jump box allows sysadmins to access ansible contains and jump to other remote desktops or virtual machines. With a jump box you can also configure settings and policies within those machines if something wwere to happen 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system health.
- Filebeat watches for any unauthorized log in attampts sending a warning to the kibana machines
- Metricbeat record the system's health such as cpu temperature, ram usage, or hard drive speeds as a machine's overload can lead to the system being shut down or a Denial of Service

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    |          | 10.0.0.5   | Linux            |
| web-2    |          | 10.0.0.7   | Linux            |
| elk-vm   |          | 10.1.0.10  | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 76.196.234.117

Machines within the network can only be accessed by the ansible container.
- Jum box 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |     No              | 10.0.0.1 10.0.0.2    |
| Web-1    |     no              | '      ' '       '   |
| Web-2    |     No              | '      ' '       '   |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- With ansible every command can be input through a playbook which automates any and all logical tasks through any webservers or hosts

The playbook implements the following tasks:
- installing docker.io so docer containers can be used in this system
- then the python3-pip is installed to make use of python scripts in the docker  module
- increasing virtual memory to make sure elk is running on its recommended requirements
- instaling the elk docker/image to launch from
- enabling the elk docker on boot to automate elk turning on when active

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Images/docker-ps-output.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.5
- Web-2 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat and Metricbeat have been installed

These Beats allow us to collect the following information from each machine:
- filebeat collects login attempts in the machine and deters if it was a sucessful one or a failed one. Metricbeat analyzes the health of a machine such as the CPU temp, RAM usage, etc.
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the fiebeat-config.yml file to filebeat.yml.
- Update the filebeat-conifg.yml file to include
 - the ip address if the elk machine and the ports used to access Kibana
- Run the playbook, and navigate to the kibana dashboard to check that the installation worked as expected.

- filebeat-install.yml is the playbook, filebeat-config.yml is copied to filebeat.yml
- Update the filebeat/metricbeat-config.yml to specify that the installation is running on the web-1 and web-2 virtual machines
- Use http://<Elk-VM-IP-Address>:5601/kibana to access the kibana dashboard

