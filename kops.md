# kops set up linux machines 
    * kops support for only AWS & GCP

## kops dependencies 
================

* domain name: dhille.shop
* create vpc: dhille.shop
* create a IAM role
    while creating ec2 machine attached 

* create a s3 bucket : dhillek8s.xyz
* create a ec2 instances
```
 apt install -y jq tree net-tools unzip  
 ssh-keygen
 cd /usr/local/bin/
 wget https://github.com/kubernetes/kops/releases/download/v1.29.0/kops-linux-arm64
 ls
 mv kops-linux-arm64 kops
 chmod 777 kops
```
##  install on kubectl 
## install kubens & kubectx install on GitHub links 

[referhere][https://github.com/ahmetb/kubectx/releases/tag/v0.9.5]



    " create a key ; name--  id_ed25519.pub "

## setup enverolment varibali 

```
    nano ~ .bashrc
```

export CLUSTER_NAME=dhille.shop
export AWS_REGION=us-east-1
export NAME=dhille.shop
export KOPS_STATE_STORE=s3://dhillek8s.xyz
export KUBE_EDITOR=nano

```
kops create cluster --name=dhille.shop --state=s3://dhillek8s.xyz --zones=us-east-1a,us-east-1b,us-east-1c \
    --node-count=3 --control-plane-count=1 --node-size=t3.medium --control-plane-size=t3.medium \
    --control-plane-zones=us-east-1a --control-plane-volume-size 10 \
    --node-volume-size 10 --ssh-public-key ~/.ssh/id_ed25519.pub --networking calico \
    --dns-zone=dhille.shop --yes
```
## delete the cluster 
```
kops delete cluster --name dhille.shop --yes
```


[def]: https://github.com/ahmetb/kubectx/releases/tag/v0.9.5