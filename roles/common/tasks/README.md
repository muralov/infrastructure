# Ansible installation on Raspberry PI
My Rasbian is based on Debian Stretch. For this I followed the installation guidelines for Debian on the page https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html


# Helm installation

Please look at the installation guides on https://github.com/peterhuene/arm-charts

An ARMv7 build of Helm can be installed manually:

$ export HELM_VERSION=v2.9.0
$ export HELM_INSTALL_DIR=~/bin
$ wget https://kubernetes-helm.storage.googleapis.com/helm-$HELM_VERSION-linux-arm.tar.gz
$ tar xvzf helm-$HELM_VERSION-linux-arm.tar.gz
$ mv linux-arm/helm $HELM_INSTALL_DIR/helm
$ rm -rf linux-arm

Initializing Helm with an ARMv7 Tiller

helm init --tiller-image=peterhuene/tiller-arm:$HELM_VERSION-arm

Additional, links https://github.com/kubernetes/helm/blob/master/docs/install.md#deleting-or-reinstalling-tiller


