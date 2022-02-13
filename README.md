# nginx-proxy-devops-challenge and Kubernetes Basics using Minikube

This project displays the basic function of nginx-reverse proxy and minikube using a Dockerfile and a helm chart

## How to use this Project

### Installation
- Install Minikube https://minikube.sigs.k8s.io/docs/start/
- Install helm     https://helm.sh/docs/intro/install/
- Install kubectl  https://kubernetes.io/docs/tasks/tools/install-kubectl/

If minikube is not reaching over internet (try pinging 8.8.8.8) follow this:
```
$ minikube ssh
$ minikube> sudo su
$ minikube> cd /etc
$ minikube> unlink resolv.conf
$ minikube> vi resolv.conf [and enter value for google nameserver: 'nameserver 8.8.8.8']
$ minikube> systemctl restart systemd-resolved

## you should be able to ping google.com now

To deploy the minikube cluster run
```
$ minikube start

Now simply run the helm chart while from root of this project
```
$ helm install nginx-proxy ./helm-chart -f ./helm-chart/values.yaml
```
To be able to test the reverse proxy, login into the kubernetes pod using the command

```
$ kubectl get pods     ########## get the pod name #####
$ kubectl exec --stdin --tty <pod_name> -- /bin/bash
$ curl http://localhost  ####this returns the creditbook.pk website ########
$ curl http://localhost:6060/ ####this returns the google.com website ########

The following project also contains a github-action yaml file which spins up a minikube cluster and deploys the helm chart to it.
