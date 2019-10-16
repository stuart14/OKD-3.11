# OKD-3.11
Ansisble script to install OKD-3.11. 

How does it work?

This uses the the OC command binaries to call Docker on a local Linux host to bootstrap a local OKD (OpenShift 3.11) containerized cluster. The ideal use case is for demo enviroments where there is a need to quickly provsion a full Openshift platform and demonstrate and test fuctionailty. The platform can be spun up in under 5 mins. Once used, the enviroment will be disposed upon reboot.

How is this diffrent to Minishift?

Minishift requires a supported type 2 hypervsior and can be "clunky". Minishift is more supported to reusable enviroments and takes care of the VM provsioning via the hypervisor

How does the Ansible script work?

The script cleans up the prevous installation, installs docker, configures firewalld for docker, configures firewalld for host external access and spins up the OpenShift cluster on docker

This has been fully tested on the following:
- Macbook running macOS Mojave 10.14.1
- CentOS 7 using CentOS-7x86_64-minimal-1908
- VirtualBox 6.0

Requirements:
- CentOS 7 and above (this will work on RedHat and Fedora although slight modifications may be required for the playbook)
- Ansible 2.6 and above
- 4GB RAM, 30GB HDD

Instructions:

This assumes you have a vanila CentOS with full updates installed and Ansible not installed 

1: Long onto a shell with root permisions or use sudo 
2: > yum install epel-release
3: > yum install ansible 
4: > cd /etc/ansible
5: > wget https://github.com/stuart14/OKD-3.11/archive/master.tar.gz
6: > tar -xvzf  master.tar.gz
7: > cd /OKD-3.11-master
8: > ansible-playbook okd.yml -v

Usage details

You can either use OC console commands or the web console

logon vai the console using > oc login -u system:admin

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





