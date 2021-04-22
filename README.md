In this project we will use ansible to configure a microsoft infrastructure with a domain controller (windows 2016), two files servers (windows 2019) and a web server (windows 2012) with IIS services. We&#39;ll use virtualbox environnement.

Our architecture will look like this:
![architecture](https://github.com/fopingn/ansible-windows-infra/blob/main/answin.png "ansible-windows-infra")

Each node is connected to two networks: one with NAT and another for internal communication.
![Nat_connection](https://github.com/fopingn/ansible-windows-infra/blob/main/virtual_net1.png)

![Private_host_connection](https://github.com/fopingn/ansible-windows-infra/blob/main/virtual_net2.png)

We assumed the following elements:

- Ansible controller is installed
- The WinRM connectivity between the hosts and the controller is fonctionnal. Useful information from ansible [here](https://docs.ansible.com/ansible/latest/user_guide/windows_winrm.html).

We&#39;ll use a master playbook (windows\_infra.yml) to configure the windows infrastructure. It contains several roles:

- addc : for configuration of an active directory domain controller (Change the hostname, Set Windows description, Create new domain in a new forest on the target host, Create group with delete protection enabled and custom attributes)
- domain\_membership: configure and join a server to domain (Change the hostname, Set Windows description, owner and organization, Configure Primary DNS Server, join server to domain, Create RDP and Admin groups locally with the use of loop in a dictionary list, Install Zabbix agent, Install Deep Security agent)
- rdp\_smb: install rdp and smb feature
- iis: Install IIS Web-Server with sub features and management tools


