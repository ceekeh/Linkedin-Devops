# Linkedin-Devops

This Repository contains information from Linkedin



 
PLAYBOOK, USING A PLAYBOOK WITH IMPORT TASK & INCLUDE TASK TO INSTALL MULTIPLE PACKAGES, FUNDAMENTAL DIFF BTW using import task and INCLUDE TASK in a playbook,
 USING IMPORT WHILE PASSING A VARIABLE  WILL FAIL/IMPORT IS USED FOR STATIC DATA  & IMPORT TASK REDUCES THE LINES OF CODE ie THAT DOES NOT CHANGE, WE CAN USE INCLUDE WHILE
 PASSING A VARIABLE & INCLUDE TASK REDUCES THE LINES OF CODE, HOW TO GET PREDEFINED & INBUILT VARIABLES USING SETUP MODULE, DEFINED VARIABLES MISSPELT ISSUES, 
 CREATING ANSIBLE ROLES, IMPORTANCE OF ANSIBLE ROLES, ANSIBLE GALAXY TO GOOGLE ALREADY CREATED ROLES, CUSTOM ROLE pass_offline, ROLE DIRECTORY STRUCTURE & CONTENT, 
 IMPORTING/ADDING FILES & REFERRING TO THE FILES IN THE ROLE DIRECTORIES, 2 LOCATIONS FOR ANSIBLE ROLES, CREATNG A CUSTOM ROLE FOR 'HTTPD',  
 CONFIGURING THE ROLE OF THE HTTPD ie ADDING HANDLERS & NOTIFIERS, SPLITTING THE PLAYBOOK ie PUTTING THE DIFF PARTS OF THE PLAYBOOK IN THE RIGHT DIRECTORY, 
 THE(ROLE)PLAYBOOK (Httpd.yml, CREATING A ROLE TO ADD A USER IN WEBSERVER, USING SHELL MODULE TO PASS USER TO SUDOERS FILE,
 THE TOMCAT ROLE WITH VARIABLE & TEMPLATE MODULE/JINJA2 WHICH WILL ADD USER & PW
 SUMMARY OF THE STEPS TO CREATE A ROLE, 3WAYS TO USE ROLES,  CREATING A ROLE WITH A TEMPLATE MODULE/JINJA2 FOR HTTPD
 
 
 
 
 



 FUNDAMENTAL DIFF BTW using import task and INCLUDE TASK in a playbook
1)When we use import task it just says
chANGed : 172.31.24.167
but when we say include task its giving us a range of information, the name of the task that is included
*********    included: /home/ansible/ansible-mc-series/05-playbooks/05-using and include/install_ java_Redhat.yml
so include is giving us more task
again we wil see more diff btw include and import
u ll use include when you want to include tasks that have variables ie task that change
2)so we use import when we are using it on static data ie does not change ie we cant use import while passing a variable, video3; we use copy module when copying static file 
3)include task is used for dynamic data, ie we can use include task while passing a variable , video; so we use template module when you are copying the dynamic files




PREDEFINED/INBUILT VARIABLE USING SETUP MODULE
 if u pass smt inside the calibres, its a variable 
so we hv some predefined variables or inbuilt variables 
an ansible os family is an inbuilt varaiable
but hw do we knw
ansible web -m setup                                   
once i run this , it will go to my server/host and it wil return info abt the server, which icludes predefined variables that i can access
 ansible_processor_cores        **** i can access this info bc its a filter
to access this i can pass it as a variable  - import_tasks: install_webserver_{{ ansible_processor_cores}}.yml


******** so we hv seen that we can create reuseable tasks but ansible actually gives us a better way to reuse our tasks and these are called roles 


 ANSIBLE ROLES
**2.02.21..   but if i hv those 2 roles but smt in role1 fails then the playbk will fail bc ansible is procedural
          *****meee... We can call more than one role in a playbook
          
Roles let you automatically load related vars,files,tasks, handlers, and other known Ansible artifacts based on a known file structure.

After you group your content in roles, you can easily reuse them and share them with other users.



ROLE DIRECTORY STRUCTURE & CONTENT
***** when a role is created, it gives you a directory structure, which will hv all these 8 directories & each dir must hv a main.yml file 

 
An Ansible role has a defined directory structure with eight main standard directories.

You must include at least one of these directories in each role. You can omit any directories the role does not use.

By default Ansible will look in each directory within a role for a main.yml file for relevant content

tasks/main.yml - the main list of tasks that the role executes.

handlers/main.yml - handlers, which may be used within or outside this role.

library/my_module.py - modules, which may be used within this role (see Embedding modules and plugins in roles for more information).

defaults/main.yml - default variables for the role. These variables have the lowest priority of any variables available, and can be easily overridden by any other variable, including inventory variables.

vars/main.yml - other variables for the role (see Using Variables for more information).

files/main.yml - files that the role deploys.

templates/main.yml - templates that the role deploys.

meta/main.yml - metadata for the role, including role dependencies



 ANSIBLE GALAXY TO GOOGLE ALREADY CREATED ROLES
45.43          if i go to google & type ansible galaxy, there are roles that hv already been created, the roles are online
*********    eg if i want to  create a role for prometheus and i just run the command without offline, its goin to download or intialize a role that is online 
so if i want to create a custom role i need to pass _offline 


                                  CUSTOM ROLE pass_offline
This is done when we want to create a custom role.

After you initialize the role, cd into the various directories and vi into the main.yml file to enter the content.



CREATING A PLAYBOOK WITH A CUSTOM HTTPD ROLE (THE ROLE DIRECTORIES) TO INSTALL HTTPD IN THE WEBSERVER
BY using the create a role command, he created & initialized a role 'httpd', the role came with all the 8 directories & he configured the role by using an existing playbook (to install httpd) he pasted the playbk in the Ansible roles dir & added handlers & notifiers to it. 
Next he split up the playbook ie putting the diff parts of the playbk in the right
directories. eg  for the handlers part , ill copy it and paste in in the handlers (main.yml) file.

 THE main.tf file IN THE TASK DIR OF THE ROLE TO INSTALL (Httpd.yml)
 After the splitting, the top part of the httpd.yml file, he copied & Pasted in the main.tf in the task dir, he changed task to roles & replaced name with httpd then run the role playbook

 CREATING A ROLE TO ADD A USER IN THE WEBSERVER
He created the role to add user & it is goin to create a grp using a grp module as seen in the main.tf file in the task dir of the add_user role
using a shell module to pass the user i just created into the sudoers file
then in the top part of the httpd.yml file in main.tf of the task dir,  he added the'user_add' role he created 
then run the role playbook


A PLAYBOOK WITH A ROLE, 'VARIABLE' & 'TEMPLATE MODULE/JINJA2' TO DYNAMICALLY REPLACE VALUES & TO ADD A USER/PW  & INSTALL TOMCAT
in continuation with video3; 

IN THE TEMPLATE DIR WE HAVE (context.xml.j2, server.xml.j2,tomcat-users.xml.j2)

tomcat-users.xml.j2:
i have a templates bc ill be passisng dynamic data, i wnat to add tomcat users, i wnat to pass the tomcat roles and PW 
SO HV copied this tomcat user.xml file and am using it as a template  and hv passed variables inside the file that will be read dynamiaclly 
thats why am using a template, template module will read dynamic data
so in the tomcat-users.xml.j2, hv passed PW,am passing 2roles, so  based on the roles that i pass here as my variables it is goin to dynamically do this
how am i passing these varaibles?
you look at your vars dir (main.yml), in there i hv all my variables for tomcat , tomcat user , PW , role , the url where am donloading my tomcat, the version, also changing 
the  tomcat port  and am changing that port in the server.xml and bc its a ginger template , i ends with .j2 
these are template files, all templates file  we use what is called ginger templating 
is a file that that accepts variables, its a dynamic file , a ginger2 file


********** in the server.xml.j2, in the connector port segment, hv passed tomcat port as a variable inside the caliibrase
it is a varaiable bc it is goin to be read at runtime 
where is it been read?? .... tomcat port, inside of my variables
i just need to cm to my variables file and change, if i want my port  to be 8000 then thats the port that tomcat will run on 
if i want to change the tomcat user name , ill change it here
so all these things will now be dynamically passed to tomcat

in the context.xml.j2
we hv the esction that has been commeted out so that we hv access to the manger, so we can log into our tomcat
 so these 3 templates are been passed when you look at the task
we hv a template for authenticating with the manger
tmeplate for configuring tomcat user credentials and roles
template for replacing default port with required port
and after we hv cahnged all these, we will notify our handler to start tomcat



STATIC AND DYNAMIC INVENTORY:

A static inventory file is a plain text file containing a list of managed hosts (just like the hostfile list we configured) or remote nodes whose numbers and IP addresses 
remain fairly constant.
On the other hand, a dynamic host file keeps changing as you add new hosts or decommission old ones.
******eg(if i go into aws and create more ec2 instance, my static file will nt change bc i hv to configure it, but if i had a dynamic inventory and i created 5more instances then
my inventory will change bc the pluggin will find and additioanl instances)
 The IP addresses of hosts are also dynamic as you stop and start new host systems. (so bc of that, that is dynamic,so you wnat an inventory that when the system changes
it will also chnage so that it gets the right ip)
