Ansible Role: Containerized Static Apache Web App
=========

The aim of this project was to write a role for deploying a static web application from Apache.
For this we took inspiration from [https://github.com/diranetafen/ansible-role-containerized-wordpress.git](https://github.com/diranetafen/ansible-role-containerized-wordpress.git) made by Dirane Tafen.

This role starts by copying the template file (templates/index.html.j2) from the site index into the user's personal directory  
("vagrant" in our case).

Then it creates a docker container in which it runs an Apache service (httpd)   
This is done by exposing port 80 and replacing the index file in the default Apache directory with the template file created previously.

Before the application is deployed, the templates/index.html.j2 file can be modified to meet specific requirements.
In fact, in this "basic" demonstration, it just displays : 
`Bienvenue sur <client_machine_name> ` 

Requirements
------------

For this role to work, it is required to have Docker and Python installed and setup.

Role Variables
--------------

This role comes with the only variable defined in defaults/main.yml:

```
system_user: vagrant
```
But it is possible to add others

Example Playbook
----------------

```
- hosts: servers
  remote_user: "{{ system_user }}"
  roles:
    - { role: ansible-role-static-apache-app }}  
```

Personal adaptations and conclusion
-----------------------------------

For the local configuration I took the liberty of adding a password for the ssh connection to the client machine and encrypting it using the ansible-vault tool.
I've also added privilege elevation to the <vagrant> user (thanks to the become: true parameter) so that it can become a super-user.

Through this mini-project I've realised that the difficulty of using a role often lies in the installation of pre-requisites and the adaptations that need to be made to set it up.

