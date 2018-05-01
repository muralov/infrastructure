# Cluster infrastructure setup

# Cluster master

 Manual steps:
 * install ansible
 * install kubernetes

# Cluster nodes

 Manual steps for odroid:
 * internet connection (wifi credentials)

 * start ssh
   * install ssh with "sudo apt install openssh-server"

 * install kubernetes

 Manual steps for raspberrypi:
 * internet connection (wifi credentials)

 * enable & start ssh
    - sudo systemctl enable ssh
    - sudo systemctl start ssh

 * install kubernetes

 Troubleshooting:  if you get an issue like this https://github.com/coreos/quartermaster/issues/79, please have a look at the solutions in this issue.


# Infrastructure setup with Minikube

# Installing minikube:

 1. Followed the link https://kubernetes.io/docs/tasks/tools/install-minikube/
   * Install kubectl
   * Install minikube
 2. Run the command: sudo minikube start --vm-driver=none

 Troubleshooting: if error occurs try to run the following commands:
 sudo kubeadm reset (delete certificates, configs of kubeadm created things)
 sudo minikube delete (delete the cluster)
 sudo rm -r ~/.minikube (delete everything of minikube)
 sudo rm -r ~/.kube (remove k8s configs)