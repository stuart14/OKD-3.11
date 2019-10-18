# OKD-3.11

Anisble script to install OpenShift (OKD-3.11) on a single Linux host. 

How does it work?

This script uses the OC command binaries(oc cluster up)to call Docker on a local Linux host to bootstrap a local OKD (OpenShift 3.11) containerized cluster and provisions a registry, router, initial templates, and a default project. The ideal use case is for demo environments where there is a need to quickly provision a full OpenShift platform and demonstrate and test functionality. The platform can be spun up in under 5 mins. Once used, the environment will be disposed upon reboot. There is no hypervisor dependency and this script has been tested running on a virtual machine in AWS Cloud, VMware ESXi and Virtual Box.

How is this different to Minishift?

Minishift requires a supported type 2 hypervisor and can be "clunky". Minishift is more supported to reusable environments and takes care of the VM provisioning via the hypervisor. Minishift actually uses the same binaries (OC command) under the hood to provision the OpenShift platform as this script.

How does the Ansible script work?

The script cleans up the previous installation, installs docker, configures firewalld for docker, configures firewalld for host external access and spins up the OpenShift cluster on docker

This has been fully tested on the following:
- Macbook running macOS Mojave 10.14.1
- CentOS 7 using CentOS-7x86_64-minimal-1908
- VirtualBox 6.0

Requirements:
- CentOS 7 and above (this will work on RedHat and Fedora although slight modifications may be required for the playbook)
- Ansible 2.6 and above
- Firewalld
- 8GB RAM, 30GB HDD (rec)

Instructions:

This assumes you have a vanilla CentOS with full updates installed and Ansible not installed 

- 1: Long onto a shell with root permissions or use sudo 
- 2: > yum install epel-release
- 3: > yum install ansible 
- 4: > cd /etc/ansible
- 5: > wget https://github.com/stuart14/OKD-3.11/archive/master.tar.gz
- 6: > tar -xvzf  master.tar.gz
- 7: > cd OKD-3.11-master
- 8: > ansible-playbook okd.yml -v

Usage details

You can either use OC console commands or the web console

logon via the console using > oc login -u system:admin

Logon on to the OpenShift web console using the ip of the host. If we say the CentOS IP was 192.168.1.140 then the URL and logon details would be:

https://192.168.1.140:8443/console

User name: Administrator
Password: any value

User name: Developer 
password: any value

Notes:

For virtual box you will need to have a bridged network for external access.

For external repos you will need to create a secret. further reading is here: 
https://medium.com/@randima.somathilaka/openshift-origin-deploying-from-external-docker-registry-part-1-9190ae301546






