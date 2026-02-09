# Linkedin-Devops

This Repository contains information from Linkedin



video 3 class34
prof manually installed ansible 

Ticket01: provision an ec2-instance in aws call ansible using ubuntu 
Search official documentation for creating aws ec2-instance


Ticket:                  ********** 17:36
  Create 3 appservers using terraform. 
  Use ansible to create ansible_user in the servers.   
***1.04 .... we can use playbooks to achieve this task 

  43:00
************* while your creating the server it comes with a default user




  ANSIBLE CONCEPTS:
1. Ansible commands:
   
    UsersMGT
    FilesMGT
    deploymentMGT
    ServicesMGT ...  the command ...........     free -m falls under sysytem mgt
    PackagesMGT

3. Ansible modules: are python scripts that can be invoke in playbooks 
   modules = ping / shell / command / apt / yum / copy

    eg
instead of using shell i can use command
i can use the command module : ansible web -m command -a "df -h" -i myhosts
OR 
i Can use only the arguments and it will still work:
ansible web -a "df -h" -i myhosts  



  ping / :
       ansible all -m ping
    command / :
       ansible all -m commad -a "ping"
       ansible all -m shell -a "ping"

       shell / :
       ansible all -m shell -a "ping"
       ansible docker -m shell -a "apt install docker.io"
    service/systemd / systemctl / :
       ansible db -m service -a "name=sshd state=restarted"
       ansible db -m systemd -a "name=httpd state=started"
copy :
 ansible app -m copy -a "src=/home/ansible/app.war dest=/opt/tomcat/webapps/"
 ansible web -m copy -a "src=/home/ansible/index.html dest=/var/www/html/"
    yum / apt / package:  
      ansible app -m yum -a "name=httpd state=present"
      ansible app -m yum -a "name=httpd state=absent"
      ansible docker -m apt -a "name=docker.i state=present"


THE DEFAULT MODULES are:
  command and setups modules 

  
3. playbooks:
============
Playbooks
  It's a configuration script written in yml. It contains plays and tasks.
  those tasks will be executed in the hosts.
4. roles  
5. Ansible galaxy   
6. Inventory = static and dynamic 


PLUGGINS   vide0 3b
 take not ethAT IN LANdmark we provison resources in aws 
so for u to use dynamic inventory to search for resources, classify and configure them bc dynamic inventory uses scripts and pluggings to classify hostfrm a cloud env or 
provider and the provider to tk note of which we use in landmark in aws 
and we can provison resources using either a static inventory file or a dynamic inventory file 
we hv a common script sthat we hv used in previous cloasses called ec2.py, its a python script and for u to use that script u need ec2.ini
with the help of these 2 scripts we can dynamically search for resources from aws , these are python scripts
but now assible can also use pluggins, we hv pluggin in ansible 

types of script:
ec2.py, and 
ec2.ini

we hv so many pluggins with ansible:
ec2   

********** if you hv this pluggin for ansible you can fetch for servers in ansible, servers in your aws account

if you run these scripts in your env, it will dynamiclaly fetch for resources in aws and classify them 
whwn we return frm our break we will see how we can use scripts and pluggins
thers are many pluggins to take advantage of but the one we will major on is ec2 bc we are goin to be configuring dynamically ec2 instances and we  will see hw ansible can 
go to our aws account and search for all our appl servers and configure them 

##






class33
cont.d frm video2

                                          WE can also use variables for apt/yum module during installion as can be seen below in setup module
1)(Apt) & yum Module
Used to install a package in the ansible client.
eg  ...  ansible all -m apt -a "name=apache2 state=present" -b       .... *** 

apache tool is not part of yum repo, so if u run it like this, you will get an error
ansible db -m yum -a "name=apache2 state=present" -b  

BUT 
we can use yum to install httpd bc httpd is a standard package name available in the default software repositories for Enterprise Linux distributions (like CentOS, RHEL, and Fedora)



  ROOT PRIVILEDGES   "-b"
41:05 ***** 

we need root priviledge to install a package & apt or yum will be used interchangeably  e.g yum for redhat and apt for ubuntu (debiem package manager) 
so we use a command called "become" to excalate our priviledges or a " -b " option , -b just means you wnat escalate the priviledges, we wnt to use sudo prividege


2) Service Module

You can use the service module to manage services running on the remote nodes managed by Ansible. This will require extended system privileges, so make sure your remote user has sudo permissions and you include the --become option to use Ansible’s privilege escalation system. Using -K will prompt you to provide the sudo password for the connecting user.


3) User Module
Used to create user accounts.  (TO create users, but you wil first craete an encrypted pW for the user)   & i bliv we need openssl for the encryption
Create a password encryption
Generate the password from your local environment
$ openssl passwd -crypt <desired_password>

4)   Setup module
This is a default module and is used to gather facts about the hosts.  egused to go to the host to gather facts, to find out wheter python has been installed, to find out
what package manager this server uses..... this is also a default module

The setup module returns detailed information about the remote systems managed by Ansible, also known as system facts.

To obtain the system facts for group1, run:

$ ansible group1 -m setup

  USING THE SETUP MODULE & VARIABLES
if i wanted to,i can use a variable to find the architecture of my server, i can use it as a filter
therfor i can use my setup module and call these variables

           DISABLING SETUP MODULE
******** we can disable this setup madule by passing  a flag called gather facts = false 
we will see hw to do that in playbks 



5)  Debug module
Executes only on the local host to display some information- message or variable value.

We do not need ssh connectivity or password for a debug module. When using the debug module, the arguments will either be
- msg = to display a message        and   - var = to display a variable
$ ansible all -m debug -a "var='This is a debug module'"             ******** it wil perform d task on my ansible control node display the msg on my ansible control node 
$ ansible all -m debug -a "msg={{}}"                                 *** so am using a debug module for info so that i can get the info y bc if am printing smt like  a file
                                                                  or perfroming a task, its been performed on the remote host, bt if i want info i can use debug so that it
                                                              prints out info on my ansible control node and with that i can pass d arguments as either variable e.g 

we can use debug mode to display these and lot of things
$ ansible all -m debug -a "var='groups'"
$ ansible all -m debug -a "var='groups.keys()'"
ansible db -m debug -a "var='ansible_os_family
 


    CUSTOM AMIs
but what ull do here, esp in your prod env goin forward, most companies wil use what is called custom AMIs, ie an AMI that hv created bc am using it for a coy, this AMI will
be managed by ansible b4 i craete the AMAI, i already exchange the key i pass in the key, the ssh key, you load it with all the software b4 you craete an instance for it
so when i introduce ansible to mg8 it i dnt nid to worry abt ssh keys anymore bc this custome AMI alraedy has a user called ansible baked in, a pecific key has already been 
exchanged so my ansible usser is already set so ill create ec2 instances based on this AMi, i can spin up a 100 instances based on this AMi.when i use that AMI , it will 
already hv been configured to be maintained by ansible but if i just hv insatnces that exists in aws then we ll see hw i can use dynamic inventory script that wil go into aws 
search tru d region, get all d inastnces and return that as an inventory then ansible wil use the ip addreses and go out and just do configuration.



   ANSIBLE PLAYBOOKS (are written in YAML) playbooks run from top to bottom & task run frm top to bottom

Playbooks can:
declare configurations
orchestrate steps of any manual ordered process, on multiple sets of machines, in a defined order
launch tasks synchronously or asynchronously
Playbooks record and execute Ansible’s configuration, deployment, and orchestration functions.

CLASS34: ansible modules are python scripts that can be invoked in a playbook

They can describe a policy you want your remote systems to enforce, or a set of steps in a general IT process.
If Ansible modules are the tools in your workshop, playbooks are your instruction manuals,(ie playbk gives ansible the instruction on what to do) and your inventory of hosts
are your raw material.  (ie these instructions always happens on your inventory, on the host that u hv defined )

At a basic level, playbooks can be used to manage configurations of and deployments to remote machines. At a more advanced level, they can sequence multi-tier rollouts 
involving rolling updates, and can delegate actions to other hosts, interacting with monitoring servers and load balancers along the way.

Playbooks are designed to be human-readable and are developed in a basic text language. There are multiple ways to organize playbooks and the files they include.


Playbooks with multiple ‘plays’ can orchestrate multi-machine deployments, running one play on your webservers, then another play on your database servers, then a third play
on your network infrastructure, and so on. (ie if u hv multiple play u can hv dif target, one play targeting db instances, the other web instances bc each play wil hv diff
arguments, it will v a host and it will hv task   *********** 1:53:20

At a minimum, each play defines two things:
the managed nodes to target, using a pattern
at least one task to execute (and this task wil hv  a module, ie what are you trying to do in this particular node) 

 Ansible task execution
When you run a playbook, Ansible returns information about connections,the name lines of all your plays and tasks, whether each task has succeeded or failed on each machine,
and whether each task has made a change on each machine.

At the bottom of the playbook execution, Ansible provides a summary of the nodes that were targeted and how they performed.

General failures and fatal “unreachable” communication attempts are kept separate in the counts.


    YAML BASICS

For Ansible, nearly every YAML file starts with a list.
Each item in the list is a list of key/value pairs, commonly called a “hash” or a “dictionary”.
So, we need to know how to write lists and dictionaries in YAML.
All YAML files can optionally begin with --- and end with ... . This is part of the YAML format and indicates the start and end of a document.
All members of a list are lines beginning at the same indentation level starting with a "- " (a dash and a space):






*********

Generated the Ansible.cfg file in the an
1)using apt module, we installed apache package manager on all the host servers (both db & web), we applied the -b root priviledge.
2)using yum module, we installed httpd package manger was installed on the web grp 
3) using service module, ngnix was installed on the db grp
4)uing the user module, created user mark & encrypted PW in the db grp

5)using the setup module:
ansible web -m setup                    ****** it will return info abt this redhat server
some of the facts returned are like variables that can be accessesed and we wil see hw to do that
   
    USING THE SETUP MODULE & VARIABLES
if i wanted to,i can use a variable to find the architecture of my server, i can use it as a filter
therfor i can use my setup module and call these variables
ill say if ansible architecture"  is  x86_64 , i can pass condition like that 
then ansible will go out bc of the setup module, it will look for servers or host that has this architecture and those are the servers that its going to perform  a task on  


6)  
   
