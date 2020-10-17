# k8s-vagrant-ansible
The poroect provides helps to set up a simple Kubernetes cluster on one machine. The cluster has 3 nodes running as VirtualBox instances - one master and two workers. It is useful for testing purposes specially for the cases where more than one node is required.

The code is mainly taken from this article: https://kubernetes.io/blog/2019/03/15/kubernetes-setup-using-ansible-and-vagrant/ hovewer some corrections were also made.

Prerequisites for running the cluster
1. [Vagrant](https://www.vagrantup.com/downloads.html)
2. [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
3. [Oracle VirtualBox](https://www.virtualbox.org/)

To start cluster use the following command:
```
      vagrant up
```      
After cluster is started use this command to ssh to master node:
```
      vagrant ssh k8s-master
```
On master use kubectl utility to manage kubernetes containers. E.g. using command like this:
```
      kubectl get pods -o wide --all-namespaces
```      
It dumps all running containers with their node and IP information.

To stop the cluster use:
```
      vagrant halt
```      
It can be resumed using **vagrant up** after.

To completely remove the cluster use:
```
      vagrant destroy -f
```      
