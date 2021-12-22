# idmDemoLab
- What does this do?
This playbook installs a full IdM demo loab

- What put yourself through this?
I needed the ability to create a lab environment to not only test updates on, but to spin up a demo lab.

- How long does this take to spin up?
Unknown as it is still a work in progress, currently around an hour.

- What environment is needed for this collection to work properly?
This collection was built assuming that you have at minimum of 3 RHEL 8 servers, a Windows server (2012+), and one Ansible machine.

- How are the server specs?
Currently the RHEL servers are 2 core, 4 gb of memory, with a 30 gb hdd. The Windows server is 2 core, 8 gb of memory, and a 60 gb hdd.

- What about the Ansible machine?
I use my laptop to run all of my Ansible playbooks off of, but you can have a dedicated machine if you wish. I would spec it the same as the RHEL servers.

- What is required to run the collection/playbook?
You must have both ansible.windows and community.windows collections installed on the Ansible machine.
To Install these collections run the following on the machine you are running Ansible on:
  - \# ansible-galaxy collection install ansible.windows
  - \# ansible-galaxy collection install community.windows

You must also run the WinRM Memory Hotfix and WinRM Setup scripts on the Window server to allow WinRM to accept connections from Ansible.
The doc is here: https://docs.ansible.com/ansible/latest/user_guide/windows_setup.html

- Are there any files that need to be changed in this?
Majority of the changes that need to be made are the variables in the inventory.yaml file.
If you deviate from this environment by having only 1 IdM server, then you will need to comment out the "Delegate IdM Zone to IdM Replica" sections in winCreate/tasks/main.yml and comment out the replica install section. This was put in here if you are running both a primary and replica IdM.

You will need to edit idmLab.yaml and uncomment subscribe-sat if you are using a local satellite, or uncomment subscribe-cdn if you are using the Red Hat CDN to patch your RHEL servers.
