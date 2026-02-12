# Linkedin-Devops

This Repository contains information from Linkedin



 
PLAYBOOK, USING A PLAYBOOK WITH IMPORT TASK & INCLUDE TASK TO INSTALL MULTIPLE PACKAGES, FUNDAMENTAL DIFF BTW  import task and INCLUDE TASK, 
 USING IMPORT WHILE PASSING A VARIABLE  WILL FAIL/IMPORT IS USED FOR STATIC DATA  & IMPORT TASK REDUCES THE LINES OF CODE ie THAT DOES NOT CHANGE, WE CAN USE INCLUDE WHILE
 PASSING A VARIABLE & INCLUDE TASK REDUCES THE LINES OF CODE, HOW TO GET PREDEFINED & INBUILT VARIABLES USING SETUP MODULE, DEFINED VARIABLES MISSPELT ISSUES, 
 ANSIBLE ROLES/ANSIBLE GALAXY, ANSIBLE GALAXY TO GOOGLE ALREADY CREATED ROLES, CUSTOM ROLE pass_offline, ROLE DIRECTORY STRUCTURE, ADDING FILES IN THE DIRECTORIES,
 CREATNG A ROLE FOR A PLAYBOOK /CONVERTING THE PLAYBOOK (httpd) TO A ROLE, CONFIGURING THE ROLE, MY NEW (ROLE)PLAYBOOK (Httpd.yml), CREATING A USER ROLE, 
 USING SHELL MODULE TO PASS USER TO SUDOERS FILE, 



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



CREATING A ROLE
BY using the create a role command, he created a role 'httpd', the role came with all the 8 directories & he configured the role by using an existing playbook (to install httpd) he pasted the playbk in the Ansible roles dir & added handlers & notifiers to it. Next he split up the playbook ie putting the diff parts of the playbk in the right
directories. eg  for the handlers part , ill copy it and paste in in the handlers (main.yml) file.

 CREATING THE 'ROLE PLAYBOOK' (Httpd.yml)
 After the splitting, the top part of the playbk he copied, he changed task to roles & replaced name with httpd then run the playbook

