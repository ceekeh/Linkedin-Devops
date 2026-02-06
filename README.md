# Linkedin-Devops

This Repository contains information from Linkedin





cont.d frm video2
    
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


3)8) User Module
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



5) Debug module


*********

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
