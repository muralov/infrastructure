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
 
 
# Installing helm
Follow this link: https://docs.helm.sh/using_helm/#installing-helm
Note: you must install helm for root as minikube runs only with root user.
 
 # Deploying the meals-planner app
 deploying meals Microservice: 
 $ helm install roles/deploy/files/meals/ --set namespace=meals-planner --name meals-release
 
 deploying planner Microservice
 $ helm install roles/deploy/files/planner/ --set namespace=meals-planner --name planner-release