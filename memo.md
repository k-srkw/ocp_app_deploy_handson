# Environment

Here is some important information about your environment:

Openshift Console: https://console-openshift-console.apps.${OCP_URL}
Openshift API for command line 'oc' client: https://api.${OCP_URL}:6443
Download oc client from http://d3s3zqyaz8cp2d.cloudfront.net/pub/openshift-v4/clients/ocp/4.9.0/openshift-client-linux-4.9.0.tar.gz

You can access your bastion via SSH:
ssh lab-user@bastion.${LAB_DOMAIN}

Make sure you use the username 'lab-user' and the password '$SSH_PASS' when prompted.

oc login -u $OCP_ADMIN -p $OCP_ADMIN_PASS https://api.${OCP_URL}:6443

# Handson

## Prerequisites

[Installing the web terminal](https://docs.openshift.com/container-platform/4.9/web_console/odc-about-web-terminal.html#odc-installing-web-terminal_odc-about-web-terminal)

## Container Execution

1. OpenShift の Worker Node へログインする

```
bash-4.4 ~ $ oc get node
NAME                                              STATUS   ROLES    AGE    VERSION
ip-10-0-139-75.ap-southeast-1.compute.internal    Ready    master   160m   v1.22.0-rc.0+894a78b
ip-10-0-142-67.ap-southeast-1.compute.internal    Ready    worker   150m   v1.22.0-rc.0+894a78b
ip-10-0-186-204.ap-southeast-1.compute.internal   Ready    master   160m   v1.22.0-rc.0+894a78b
ip-10-0-191-87.ap-southeast-1.compute.internal    Ready    worker   149m   v1.22.0-rc.0+894a78b
ip-10-0-193-61.ap-southeast-1.compute.internal    Ready    master   160m   v1.22.0-rc.0+894a78b

bash-4.4 ~ $ oc debug node/ip-10-0-142-67.ap-southeast-1.compute.internal
Starting pod/ip-10-0-142-67ap-southeast-1computeinternal-debug ...
To use host binaries, run `chroot /host`
Pod IP: 10.0.142.67
If you don't see a command prompt, try pressing enter.

sh-4.4# chroot /host
```

2. Podman でコンテナを起動する

```
sh-4.4# podman run --rm -it ubuntu /bin/bash
Resolved "ubuntu" as an alias (/etc/containers/registries.conf.d/000-shortnames.conf)
Trying to pull docker.io/library/ubuntu:latest...
Getting image source signatures
Copying blob 7b1a6ab2e44d done  
Copying config ba6acccedd done  
Writing manifest to image destination
Storing signatures

root@961d955f1219:/# cat /etc/os-release | head -n 3
NAME="Ubuntu"
VERSION="20.04.3 LTS (Focal Fossa)"
ID=ubuntu

root@961d955f1219:/# ps auxww
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.0   4116  3528 pts/0    Ss   05:32   0:00 /bin/bash
root          11  0.0  0.0   5904  2876 pts/0    R+   05:34   0:00 ps auxww

root@961d955f1219:/# dpkg -l | wc -l
97

root@961d955f1219:/# ls /boot/

root@961d955f1219:/# uname -r
4.18.0-305.19.1.el8_4.x86_64

root@961d955f1219:/# exit
exit

sh-4.4# exit
exit
sh-4.4# exit
exit

Removing debug pod ..
```

2. 