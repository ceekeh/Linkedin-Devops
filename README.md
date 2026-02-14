# Linkedin-Devops

This Repository contains information from Linkedin



 
PLAYBOOK, USING A PLAYBOOK WITH IMPORT TASK & INCLUDE TASK TO INSTALL MULTIPLE PACKAGES, FUNDAMENTAL DIFF BTW using import task and INCLUDE TASK in a playbook,
 USING IMPORT WHILE PASSING A VARIABLE  WILL FAIL/IMPORT IS USED FOR STATIC DATA  & IMPORT TASK REDUCES THE LINES OF CODE ie THAT DOES NOT CHANGE, WE CAN USE INCLUDE WHILE
 PASSING A VARIABLE & INCLUDE TASK REDUCES THE LINES OF CODE, HOW TO GET PREDEFINED & INBUILT VARIABLES USING SETUP MODULE, DEFINED VARIABLES MISSPELT ISSUES, 
 CREATING ANSIBLE ROLES, ANSIBLE GALAXY TO GOOGLE ALREADY CREATED ROLES, CUSTOM ROLE pass_offline, ROLE DIRECTORY STRUCTURE & CONTENT, 
 IMPORTING/ADDING FILES & REFERRING TO THE FILES IN THE ROLE DIRECTORIES, 2 LOCATIONS FOR ANSIBLE ROLES, CREATNG A CUSTOM ROLE FOR 'HTTPD',  
 CONFIGURING THE ROLE USING THE HTTPD PLAYBOOK & ADDING HANDLERS & NOTIFIERS, SPLITTING THE PLAYBOOK ie PUTTING THE DIFF PARTS OF THE PLAYBOOK IN THE RIGHT DIRECTORY, 
 THE(ROLE)PLAYBOOK (Httpd.yml, CREATING A ROLE TO ADD A USER IN WEBSERVER, USING SHELL MODULE TO PASS USER TO SUDOERS FILE,
 THE TOMCAT ROLE WITH VARIABLE & TEMPLATE MODULE/JINJA2 WHICH WILL ADD USER & PW
 SUMMARY OF THE STEPS TO CREATE A ROLE,  CREATING A ROLE USING  the template module httpd playbook.



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



CREATING A CUSTOM HTTPD ROLE & THE DIRECTORIES
BY using the create a role command, he created & initialized a role 'httpd', the role came with all the 8 directories & he configured the role by using an existing playbook (to install httpd) he pasted the playbk in the Ansible roles dir & added handlers & notifiers to it. 
Next he split up the playbook ie putting the diff parts of the playbk in the right
directories. eg  for the handlers part , ill copy it and paste in in the handlers (main.yml) file.

 CREATING THE 'ROLE PLAYBOOK' (Httpd.yml)
 After the splitting, the top part of the playbk he copied, he changed task to roles & replaced name with httpd then run the playbook

 CREATING A ROLE TO ADD A USER IN WEBSERVER
He created the role & it is goin to create a grp using a grp module as seen in the task dir of the add_user role
then in the top part of the httpd playbk (Httpd.yml),  he added the'user_add' role he created 
