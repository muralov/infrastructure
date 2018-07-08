# Cluster infrastructure setup

# Cluster master

 Manual steps:
 * install ansible
 * install kubernetes

# Cluster nodes

 Manual steps for odroid:
 * internet connection (wifi credentials)

 * start ssh
   * install ssh with $ sudo apt install openssh-server

 * install kubernetes

 Manual steps for raspberrypi:
 * internet connection (wifi credentials)

 * enable & start ssh
    - $ sudo systemctl enable ssh
    - $ sudo systemctl start ssh

 * install kubernetes

#### Troubleshooting
  
 In case kube-proxy pod on odroid or raspberrypi doesn't run, try to apply daemonset-arm64.yaml on odroid and daemonset-armhf.yaml on raspberry, which should fix it. Please also look at the issue https://github.com/coreos/quartermaster/issues/79.

# Infrastructure setup with bare metal

* Creating k8s cluster with raspberrypi as master and odroid as worker node

$ ansible-playbook playbook.yml --ask-become-pass --tags "k8s.cluster" -i hosts  
and some manual described in the command's result. Install waeave plugin here too.

After that, you have to create a DeamonSet for odroid similar to files/deamonset-arm64.yaml in the project: oc create -f {odroid arm64 dameonset yaml}. After that you should join the odroid node. Everything is exactly described here: https://gist.github.com/squidpickles/dda268d9a444c600418da5e1641239af

# Infrastructure setup with Minikube

# Installing minikube:

 1. Followed the link https://kubernetes.io/docs/tasks/tools/install-minikube/
   * Install kubectl
   * Install minikube
 2. Run the command: $ sudo minikube start --vm-driver=none
 3. root user must be used: $ sudo su && kubectl get pods

 Troubleshooting: if error occurs try to run the following commands:
 $ sudo kubeadm reset (delete certificates, configs of kubeadm created things)
 $ sudo minikube delete (delete the cluster)
 $ sudo rm -r ~/.minikube (delete everything of minikube)
 $ sudo rm -r ~/.kube (remove k8s configs)
 
 
 # Ansible Tasks
 
 ## Installing the minikube
 ansible-playbook playbook-minikube.yml --ask-become-pass --tags "minikube"
 
 ## Initialize the minikube
  
 ansible-playbook playbook-minikube.yml --ask-become-pass --tags "helm.init"
 
 If helm is not installed yet, you have to install the helm with: 
 $ ansible-playbook playbook-minikube.yml --ask-become-pass --tags "helm.install"  or to do both install and init run $ ansible-playbook playbook-minikube.yml --ask-become-pass --tags "helm"      
 
 
 ## Deploying and undeploying the meals-planner app with Helm
 
 ansible-playbook playbook-minikube.yml --ask-become-pass --tags "deploy.helm"
 
 ansible-playbook playbook-minikube.yml --ask-become-pass --tags "deploy.helm" -e "delete=true"
 
 ## with kubectl
 
 ansible-playbook playbook-minikube.yml --ask-become-pass --tags "deploy.kubectl"
 
 ansible-playbook playbook-minikube.yml --ask-become-pass --tags "deploy.kubectl" -e "delete=true"