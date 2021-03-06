List the helm chart

root@XXXXX:~# helm list 

NAME               	REVISION	UPDATED                 	STATUS  	CHART                	NAMESPACE  

glance             	1       	Thu May  3 17:02:03 2018	DEPLOYED	glance-0.1.0         	openstack  

heat               	1       	Thu May  3 16:56:25 2018	DEPLOYED	heat-0.1.0           	openstack  

horizon            	1       	Thu May  3 16:58:49 2018	DEPLOYED	horizon-0.1.0        	openstack  

ingress-kube-system	2       	Fri May  4 13:11:06 2018	DEPLOYED	ingress-0.1.0        	kube-system

ingress-openstack  	2       	Fri May  4 13:11:07 2018	DEPLOYED	ingress-0.1.0        	openstack  

keystone           	1       	Thu May  3 15:41:01 2018	DEPLOYED	keystone-0.1.0       	openstack  

kube-dns           	1       	Thu May  3 14:50:49 2018	DEPLOYED	kube-dns-0.1.0       	kube-system

libvirt            	1       	Fri May  4 01:36:05 2018	DEPLOYED	libvirt-0.1.0        	openstack  

mariadb            	1       	Thu May  3 15:25:36 2018	DEPLOYED	mariadb-0.1.0        	openstack  

memcached          	1       	Thu May  3 15:33:55 2018	DEPLOYED	memcached-0.1.0      	openstack  

neutron            	1       	Fri May  4 01:43:28 2018	DEPLOYED	neutron-0.1.0        	openstack  

nfs-provisioner    	1       	Thu May  3 15:23:37 2018	DEPLOYED	nfs-provisioner-0.1.0	nfs        

nova               	1       	Fri May  4 01:43:25 2018	DEPLOYED	nova-0.1.0           	openstack  

rabbitmq           	1       	Thu May  3 15:32:44 2018	DEPLOYED	rabbitmq-0.1.0       	openstack  

tiller             	1       	Thu May  3 14:51:04 2018	DEPLOYED	tiller-0.1.0         	kube-system


Removing the helm chart:-
========================
set -X; for i in $(helm list | awk '{print $1}'); do helm delete $i --purge; done

release "heat" deleted
release "horizon" deleted
release "ingress-kube-system" deleted
release "ingress-openstack" deleted
release "keystone" deleted
release "kube-dns" deleted
release "libvirt" deleted
release "mariadb" deleted
release "memcached" deleted
release "neutron" deleted


root@XXXXX:~# kubectl get pods -n kube-system

NAME                              READY     STATUS    RESTARTS   AGE
etcd-megam-2                      1/1       Running   0          13d
kube-apiserver-megam-2            1/1       Running   0          13d
kube-controller-manager-megam-2   1/1       Running   0          13d
kube-proxy-jwcvx                  1/1       Running   0          13d
kube-scheduler-megam-2            1/1       Running   0          13d

sudo systemctl stop kubelet

sudo systemctl disable kubelet

Removing the containers:-
=======================
sudo docker ps -aq | xargs -r -L1 -P16 sudo docker rm -f

sudo rm -rf /var/lib/openstack-helm/*

sudo rm -rf /var/lib/nova/*

sudo rm -rf /var/lib/libvirt/*

sudo rm -rf /etc/libvirt/qemu/*

sudo findmnt --raw | awk '/^\/var\/lib\/kubelet\/pods/ { print $1 }' | xargs -r -L1 -P16 sudo umount -f -l

root@XXXXXX:~# docker ps -a

CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

If any pods not removed properly

kubectl delete pods nova-cell-setup-1525424400-cjdwb -n openstack

root@XXXXX:~# kubectl get pods --all-namespaces

NAMESPACE     NAME                              READY     STATUS    RESTARTS   AGE

kube-system   etcd-megam-2                      1/1       Running   0          13d

kube-system   kube-apiserver-megam-2            1/1       Running   0          13d

kube-system   kube-controller-manager-megam-2   1/1       Running   0          13d

kube-system   kube-proxy-jwcvx                  1/1       Running   0          13d

kube-system   kube-scheduler-megam-2            1/1       Running   0          13d
