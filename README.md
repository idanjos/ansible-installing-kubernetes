# ansible-installing-kubernetes
I havent seen a guide where it was possible to automatically install and configure Kubernetes clusters. I decided to share what I cameup with using Ansible. I have collected important tasks and developed ansible playbooks which will configure 2+ VMs into a Master/Worker Kubernetes cluster.
The hosts are in the hosts file, and each host has their own file in host_vars where you can configure the ssh connection, location and their worker_name. The cluster will not accept nodes with the same name.
In the group_vars/all, you can define the subnetwork of the cluster and the define the version of kubernetes you want to use.

The pre requirements:

	. 3 available VMs/machines, 1 master 2 workers
	. python installed in the VMs/machines
	. Defining static IPs to the VMs/machines
	. 4th VM/machine which will run the ansible playbooks(python and ansible required!)
	

Before diving in, this repo has by default,
   Static IPs
	. Master: 192.168.10.10 -u ubu -p ubu
	. Worker1: 192.168.10.11 -u ubu -p ubu
	. Worker2: 192.168.10.12 -u ubu -p ubu

  Kubernetes Version
	. 1.19.0-00

  Cluster network
	. 10.10.0.0/24

Disclamer:
	
	The repo was tested on VMs

1)

	ansible-playerbook -i inventories/tst/ site_infra.yml

This is will playbook site_infra.yml which will import and run the require playbooks to configure and install kubernetes. 

2) On the master VM

	kubectl get nodes

should appear both master and worker nodes.

Resources:
https://github.com/justmeandopensource/kubernetes/blob/master/docs/install-cluster-ubuntu-20.md
https://www.digitalocean.com/community/tutorials/how-to-create-a-kubernetes-cluster-using-kubeadm-on-ubuntu-16-04  
