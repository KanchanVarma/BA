#Image of ubuntu as a builder
FROM ubuntu:18.04

#Updating the apt-get packages
RUN apt-get update

#Installing the vim editor
RUN apt-get install -y vim

#Installing the package sudo
RUN apt-get install -y sudo

#Installing ansible packages to run and deploy application inside container
RUN apt-get install -y ansible

#Adding the ansible scripts from the host to the container for "ba"
ADD ansible_scripts_ba ansible_scripts_ba

#Adding the releases folder containing the config and the executable files of "ba"
ADD releases/ba releases

#Adding the services folder containing the "ba" conf
ADD services services

#changing the working directory
WORKDIR ansible_scripts_ba

#Executing the ansible-playbook to deploy the sevice files
RUN ansible-playbook -i hosts add_services.yml -c local

#Executing the ansible-playbook to deploy the "ae" application
RUN ansible-playbook -i hosts  ba_deploy.yml  -c local

EXPOSE 8083

WORKDIR /huda/ba

CMD ["./ba"]
