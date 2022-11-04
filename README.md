# ansible

## Ansible: A CM Tool and the latest version of 6.0

Ansible 6.0 is Python3 based and installation of Python 3 is needed

### Inventory : This is the file which we supply ansible the list of DNS names or IP's on the machine that you would like to do that configuration management. 

## The default group in this file is 'all' which is included all the DNS or IP's that you supplied

### Ansible can be operated in 2 ways

 * Manual way : Executing the commads and can work one command at a time
 * Automated wat - Using Ansible Playbook

 ### Samble Ansible Manual Command

 ansible all -i inv -e ansible_user=centos -e ansible_password=DevOps321 -m shell -a uptime

-i                  : Inventory file
all                 : Group Name
ansible_user        : Username which ansible uses for authentication
ansible_password    : Password which ansible uses for authentication
-m                  : Module
-a                  : Argument
-e                  : Extra Arguments

PS : ansible --help gives all the latest and greates option of that time

### Pre-Requisites:
    The very first thing to ensure that ANSIBLE works is : SSH your ansible should be able to ssh to the enteries mentioned in your inventory file.

## Manual Command
    ansible dev -i inv -e ansible_user=centos -e ansible_password=DevOps321 -m shell -a uptime

### Playbooks is nothing but your ansible scripts which are writted on YAML 

YAML    : This is just a Markup language ( Markup language is nothing but presentation laguage)

Abbrevation of YAML : yet another markup language

# YAML Basics : 
    * Dictionary : A key value pair is called as dictionary
    * List        : A key with multiple values is called as a list ( when we use list iy has to start with -)
    * Map         : A key with multiple key value pairs is referred as MAP

## PS : YAML is intendation specific ( Spacing Matters)

| indicates multi line input

### What is a Playbook in ansible ??

Playbook is a list of plays
What is a Play? A Play is a list of tasks
What is a Task? A Task is an action or actions that you wish to do

# Ansible playbooks should always end with .yml or .yaml. Anything apart from that won't be considered.


### How to run the Ansible play book?

ansible-playbook -i inv -e ansible_user=centos -e ansible_password=DevOps321 01-sample.yml

ansible-playbook -i inv -e ansible_user=centos -e ansible_password=DevOps321 -e COMPONENT=catalogue roboshop.yml

### When to use remote_src
# When we say remote_src yes the download happens on the remote machine. If this is not mentioned download happens on the same machine on which we run the command.

### How do you prevent a service from restarting?
# We use handlers to perform this

### FOR LOOP

## To run a loop we use FOR loop

for i in mongodb catalogue redis cart user mysql shipping frontend; do ansible-playbook -i inv -e ansible_user=centos -e ansible_password=DevOps321 -e COMPONENT=$i roboshop.yml; done

With Environments,

git pull ; for i in mongodb catalogue redis cart user mysql shipping rabbitmq payment frontend; do ansible-playbook -i dev-inv -e ansible_user=centos -e ansible_password=DevOps321 -e ENV=dev -e COMPONENT=$i roboshop.yml; done


# for i in mongodb catalogue redis mysql cart frontend ( Any component can be mentioned here)

Catalogue component's dependency is MongoDB -- It can be done using meta argument inside the  meta argument. Meta argument helps you always in creating such dependencies. 

#### Ansible-Pull
 
 for Ansible pull to work you need to ensure that the machine which executes gthe pull command has Ansible Installed

 ## Install Ansible: curl https://gitlab.com/thecloudcareers/opensource/-/raw/master/lab-tools/ansible/install.sh | sudo bash

 ### ANSIBLE TAGS

 ansible-playbook 13-tags.yml  --skip-tags  web
ansible-playbook 13-tags.yml  -t web