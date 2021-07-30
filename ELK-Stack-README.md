## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/mendmar/ELK-STACK-PROJECT/blob/main/Diagrams/ELKSTACK_PROJECT.PNG

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the project file may be used to install only certain pieces of it, such as Filebeat.

Link for the playbook:
https://github.com/mendmar/ELK-STACK-PROJECT/blob/main/Ansible/elk-playbook.txt

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly secure, in addition to restricting access to the network.
-What aspect of security do load balancers protect? What is the advantage of a jump box? The load balancer acts as a proxy firewall with a set of rules that can limit or completely deny access to the web servers. The advantage of a Jump box is to not give access to the web servers, if something should happen to the Jump Box the web servers will still be up and running. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system applications.
What does Filebeat watch for? It monitors any changes or any problems to the logs and servers. 

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
| Jump Box | Gateway | 10.0.0.4 | Linux |
| Web-1    | Server  | 10.0.0.5 | Linux |
| Web-2    | Server  | 10.0.0.6 | Linux |
| ELK-VM   | Server  | 10.2.0.4 | Linux |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump_Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 20.85.235.216 
Whitelisted IP addresses: 142.129.208.175

Machines within the network can only be accessed by the Admin.
Which machine did you allow to access your ELK VM? What was its IP address? Only the Jump Box can access the ELK-VM, it's IP is 10.0.0.5.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No | 10.0.0.4 |
| Web-1    | No     | 10.0.0.4 |
| Web-2    | No     | 10.0.0.4 |
| ELK-VM   | No     | 10.0.0.4 |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because all the containers were already configured and ready for download.

What is the main advantage of automating configuration with Ansible? The chance of error is reduced, and it is also more efficent to run these container, if there is a problem with anything, it is readily and easily fixed.

The playbook implements the following tasks:
- update the ansible-config.yml to include ELK.
- update host file to include ELK.
- update the elk-config.yml
- install the container using the playbook: elk-playbook.yml

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/mendmar/ELK-STACK-PROJECT/blob/main/Ansible/elk_docker_ps.PNG

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6

We have installed the following Beats on these machines:
- Filebeats
- Metricbeats (coming soon)

These Beats allow us to collect the following information from each machine:
- Filebeat monitors and collects any change to the log files on these servers. An example would be syslog, this is ELK outputting to the log file the current event s to date.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk-config.yml file to ansible container, here to will create a files directory to store it in (make sure to move the file to the files directory).

- Update the elk-config file to include the Private IP of your ELK server. 

- Run the playbook, and navigate to web server Public IP to check that the installation worked as expected. Check to see if Kibana is loaded, if it has then it was successful.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_ The playbook is labeled: elk-playbook.yml, in the repository it is a .txt file for easy downloads. In order to run it you must create a filebeat roles directory within you ansible container.

- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? To make ansible run the playbook first you need to add the ports to the elk-config.txt file. The changes that need to be made to to the default 10.0.0.12 private IP, here you replace these IP's with the new values from your machines. This is the only change you have to make, changing anything else can cause the file to break.

- _Which URL do you navigate to in order to check that the ELK server is running? http://13.66.134.199:5601/app/kibana#/discover?_g=(filters:!())&_a=(columns:!(_source),filters:!(('$state':(store:appState),meta:(alias:!n,disabled:!f,index:'filebeat-*',key:message,negate:!f,params:(query:'rtnl:%20received%20neighbor%20for%20link%20!'3!'%20we%20don!'t%20know%20about,%20ignoring.'),type:phrase),query:(match_phrase:(message:'rtnl:%20received%20neighbor%20for%20link%20!'3!'%20we%20don!'t%20know%20about,%20ignoring.')))),index:'filebeat-*',interval:auto,query:(language:kuery,query:''),sort:!(!('@timestamp',desc)))