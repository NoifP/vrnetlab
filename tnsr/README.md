# TNSR VM

Download TNSR iso from NetGate. Convert it to qcow2 to via 'dirty magic' (install it in a proxmox vm and then convert the installed disk).

1. Create a VM in proxmox using the TNSR iso
1. Just add 1 NIC (virtio) for now (for management/install)
1. 20GB Disk. During install disable LVM - it isn’t useful in this scenario.
1. During instal set the network as follows:

    * IP address: 10.0.0.15/24
    * Gateway: 10.0.0.2
    * DNS 9.9.9.9

```bash
qemu-img convert -O qcow2 -f raw  /dev/zvol/rpool/data/vm-102-disk-0 /tmp/TNSR-23.11-3.qcow2
```

Once the qcow2 image is downloaded, build the container with the following command:

```bash
make
```

The resulting container will be tagged as `vrnetlab/netgate_tnsr:<version>`, e.g. `vrnetlab/netgate_tnsr:23.11-3`.

## Host requirements

* 4 vCPU, 16GB RAM

## Configuration

* once it is running telnet to the management ip on port 5000 (this is the serial console on the tnsr box)
* change the network interface name in `/etc/netplan/50-tnsr-host-interfaces.yaml` to be enp1s0 and then do `sudo netplan apply` - you should be able to ssh to the management IP now and get tnsr login.