# okd4_files

See https://medium.com/swlh/guide-okd-4-5-single-node-cluster-832693cb752b for full guide.  Below pushit and wrapit scripts are just commands from guide.

Pull the branch
- git clone -b snc https://github.com/gtam/okd4_files.git

Rename and edit files as needed

Run the pushit script to install components
- okd4_files/pushit

Startup bootstrap, control-plane, and worker nodes
- set them up according to guide by interrupting the ISO startup and append
```
ip=10.1.24.209::10.1.0.1:255.255.255.0:::none \
nameserver=10.1.24.200 coreos.inst.install_dev=/dev/sda \
coreos.inst.image_url=http://10.1.24.200:8080/okd4/fcos.raw.xz \
coreos.inst.ignition_url=http://10.1.24.200:8080/okd4/bootstrap.ign
```

OR

- boot from CD and run the following for bootstrap; then master

```
UUID=`nmcli con sh|grep conn|awk '{print $4}'`
nmcli con mod $UUID ipv4.address x.x.x.x/x
nmcli con mod $UUID ipv4.gateway x.x.x.x
nmcli con mod $UUID ipv4.dns x.x.x.x
nmcli con mod $UUID ipv4.dns-search domain.local
nmcli con mod $UUID ipv4.method manual
nmcli con down $UUID
nmcli con up $UUID
```
```
sudo coreos-install install /dev/sda \
--copy-network --insecure-ignition \
--ignition-url http://10.1.24.200:8080/okd4/bootstrap.ign \
--image-url http://10.1.24.200:8080/okd4/fcos.raw.xz
```
```
init 6 #Reboot
```
- Check bootstrap progress
```
[okd4-services ~]# watch -n10 netstat -pnt
```
```
[root@okd4-services ~]# openshift-install --dir=install_dir/ wait-for bootstrap-complete --log-level=debug
```

Run the wrapit script to finish the rest of steps
- okd4_files/wrapit
