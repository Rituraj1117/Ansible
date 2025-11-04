**HOW TO SETUP AND CONFIGURATION ANSIBLE, ANSIBLE PLATBOOK?**



**Step 1. Install Ansible Package on Ubuntu VMs**

**Add Ansible PPA** 

**# add-apt-repository ppa:ansible/ansible**

**# apt update** 

**# apt install ansible -y**





**Step2. Check the Version, all configuration file related ansible.**

**# ansible --version**

**# ls -l /etc/ansible**

**# cd /etc/ansible**

**ansible.cfg, hosts, roles**



**Step3. Create ansible user on Server VMs,** 

**NOTE: Create an ansible user on both the Ansible server and the node machines, then configure password less sudo access using the visudo file.**

**here create ansible user all VMs.** 

**useradd ansible-user**

**passwd ansible-user**



**NOTE: Grant Passwordless direct access to the ansible user in the visudo file.**





**Step4. Generate the Key on Ansible server and copy the key all nodes.**

**# ssh-keygen  ==> on ansible server machine.**

**# cd /home/ansible-user.ssh/**



**Here copy the key all ansible nodes**

**ssh-copy-id username@ips**

**# ssh-copy-id ansible-user@192.168.1.1**

**# ssh-copy-id ansible-user@192.168.1.2**



**NOTE: IF is not copy than copy forcefully** 

**# ssh-copy-id ansible-user@192.168.1.1 -f**  



**Remove the Old key** 

**# ssh-keygen -R 192.168.1.1**





**Step5. Create Directory require VMs, like production, testing vms, cloud VMs etc.**

**mkdir -p /home/ansible-user/production-server**



**Inside create inventory files**

**touch production\_server.ini** 

**Inside write inventory host (host) this host name is confgigure to /etc/ansible/hosts file because easily access node.**



**\[Ansible-servers]**

**192.168.1.1 ansible\_ssh\_private\_key\_file=~/.ssh/id\_rsa**

**192.168.1.2 ansible\_ssh\_private\_key\_file=~/.ssh/id\_rsa**

**192.168.1.3 ansible\_ssh\_private\_key\_file=~/.ssh/id\_rsa**

**192.168.1.4 ansible\_ssh\_private\_key\_file=~/.ssh/id\_rsa ansible\_python\_interpreter=/usr/bin/python2**





**\[all:vars]**

**ansible\_python\_interpreter=/usr/bin/python3**

**ansible\_user=ansible\_ipa**

**ansible\_ssh\_private\_key\_file=/home/ansible\_ipa/.ssh/id\_rsa**







**Step6. Mentions Nodes/inventory node in /etc/ansible/hosts configuration file.**

**### This is production server of vms**

**\[Ansible-servers]** 



 

**Step7. Give the some access /etc/ansible/ansible.cfg configuration file.**

**The /etc/ansible/ansible.cfg file is used to configure Ansible's behavior, such as default inventory, sudo options, and more.**





**\[defaults]**



**# some basic default values...**



**inventory      = /etc/ansible/hosts**

**#library        = /usr/share/my\_modules/**

**#module\_utils   = /usr/share/my\_module\_utils/**

**#remote\_tmp     = ~/.ansible/tmp**

**#local\_tmp      = ~/.ansible/tmp**

**#plugin\_filters\_cfg = /etc/ansible/plugin\_filters.yml**

**#forks          = 5**

**#poll\_interval  = 15**

**sudo\_user      = root**

**#ask\_sudo\_pass = True**

**#ask\_pass      = True**

**#transport      = smart**

**#remote\_port    = 22**

**#module\_lang    = C**

**#module\_set\_locale = False**

**ansible\_python\_interpreter=/usr/bin/python3.8**





**Step8. Check the Connectivity in group of hosts.**

**# ansible -i inventory.ini-name  (host\_name) -m ping** 

**# ansible -i production.ini ansible-server -m ping** 







**Step**

**Step**



**ANSIBLE COMMANDS:**

**Check Version:**

**ansible --version**

**ansible all -m ping**



**Check the connectivity all node inside of inventory file.**

**# ansible -i inventory.ini-name  (host\_name) -m ping**

**ansible -i production.ini ansible-server -m ping**





















