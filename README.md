# IdM lab automation
- What does this do?
This playbook will call roles/plays from ansible-freeipa, rhel-system-roles, and local to create an IdM lab that will have both a primary and replica IdM server with integrated DNS and CA. It will promote a Windows server to a DC, Domain Controller. It will create; users and groups in both AD and IdM, a trust between AD and IdM, HBAC and SUDO rules, 

- What put yourself through this?
I needed the ability to create a lab environment to not only test updates on, but to also spin up a demo lab for customers.

- How long does this take to spin up?
In my lab it takes less then an hour to install and configure everything. But your time may vary depending on the hardware you are using.

- What environment is needed for this collection to work properly?
This collection was built assuming that you have at minimum of 3 RHEL 8 servers, a Windows server (2012+), and one ansible host.

- How are the server specs?
Currently all servers have 2 cores and 4 gb of memory. The RHEL servers have 30 GB of space and the Windows server has 60 GB.

- What about the Ansible machine?
I use my laptop to run all of my Ansible playbooks off of, but you can have a dedicated machine if you wish or use one of the 3 RHEL machines.

- What is required to run the collection/playbook?
You must have a few collections installed to have this work:
For Windows to work you must have both ansible.windows and community.windows collections, and for RHEL you need rhel-system-roles and ansible-freeipa installed on the Ansible host.
To Install these collections run the following on the machine you are running Ansible on:
  - \# ansible-galaxy collection install ansible.windows
  - \# ansible-galaxy collection install community.windows
  - \# dnf install ansible-freeipa rhel-system-roles -y

For some versions of Windows you must also run a few powershell scripts on the Window server to allow WinRM to accept connections from Ansible.
The doc is here: https://docs.ansible.com/ansible/latest/user_guide/windows_setup.html

- Are there any files that need to be changed in this?
Changes that need to be made are the variables in the inventory file. You can choose to skip items like the configuring Windows or installing replica by using --skip-tags when run.

- What are the tags used?
I have a few tags so you can call what you want to use.
  win - windows (DC, users, groups, & DNS delegation)
  locUsers - local users
  cdn - Red Hat CDN
  satloc - Local Satellite
  replica - IdM replicas
  clients - IdM clients
  adtrust - AD Trust
  idmUsers - IdM users
  idmGrps - IdM groups
  hostGrp - hostgroup
  hbac - HBAC rules
  sudo - SUDO rules and enable IdM sudo on clients

