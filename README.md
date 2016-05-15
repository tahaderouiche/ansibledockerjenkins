Jenkins on a Docker container launched via Ansible
===========

This is a guide for anyone who needs to run Jenkins on a Docker container, with persistant data (using Docker data container) and with a complete playbook to prepare the environment.

## Content
The repository contains the below files:   
1. docker-jenkins.yml: Main Ansible playbook to deploy all required packages and files to install and set up Docker and run Jenkins on top of it.   
2. hosts: contains the list of hosts targetted by Ansible during the deployment process.   
3. config.xml: config files used by Ansible to define paths for hostfile and roles.  
4. Docker: Folder containing docker file and other files required to launch Build Jenkins Docker container. It is based mainly on the original Jenkins docker file with some small changes.  
5. jenkins_data: Folder containing docker file that will be used to build the docker image of the data container used to keep data persistent.  
6. get-details.yml: Playbook used to retreive the Administator assword after the first intallation of Jenkins.  
7. start-jenkins.yml: Playbook used to start Jenkins container again (after a crash for example)  
8. roles: contains the two roles called by the main Anisble playbook.  
  * prepare/tasks/main.yml: This will install all required packages and files as prerequisites to Docker and finally install docker.  
  * jenkins/tasks/main.yml: Will install a Docker data container and Docker Jenkins container after building an image for both of these. The data container will be mounted to Jenkins container to make data persistent, ie a crash/stop of Jenkins container will not result in a loss of data/jobs/configuration.   
## Requirements:
This was tested using ansible 2.0.2.0, and target server is Ubuntu 14.04

## How to use it
1. Clone the repository.
2. Edit hosts file with the exact hostname, port and path to the private key.
3. Run `ansible-playbook docker-jenkins.yml` . This will set up all required packages and install jenkins to run on port 8081.
4. Once Jenkins is up and running, you can confirm by going to <hostname>:8081. For a first installation, this will require an admin password. Run `ansible-playbook get-details.yml` and copy the password that will appear.
5. You can complete the installation by selecting the right plugins and start using Jenkins.

## More details:
Docker file used for Jenkins is based on the official one that can be found [here] (https://github.com/jenkinsci/docker)
Ansible playbook tasks are based on the steps defined on the official docker docs [here] (https://docs.docker.com/engine/installation/linux/ubuntulinux/)
