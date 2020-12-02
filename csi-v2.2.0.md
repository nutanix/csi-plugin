Quick start guide

# LVM Volume supporting multi vdisks volume group

LVM uses I/O striping to provide improved performance. This will be perfect for running
workloads which need high IO performance. 

You may need to install lvm2 package and/or its dependencies for using this feature.
For example in centos, execute *yum install lvm2*.

Please refer to example/ABS/sc-lvm.yaml for LVM storage-class example.

# NFS dynamic share provisioning

This fetaure requires use of Nutanix Files product. CSI volume driver dynamically provisions a new share on the target file server with the limits specified in the persistent volume claim (PVC). With NFS you have ReadWriteMultiple capability.

Please refer to example/AFS/dyn-nfs-sc.yaml for storage class example.

# iSCSI Auto CHAP Authentication

This feature enables iSCSI CHAP authentication. CHAP password is automatically generated while setting up iSCSI session. So this provides security with no added complexity.

Enable this feature by setting *chapAuth: ENABLED* in storage class parameters.


