# SLES 15SP1

Support Nutanix CSI driver running on SUSE Linux Enterprise Server 15SP1 (SLES 15SP1). 

## Support ABS

Install iSCSI Initiator package on each worker node for being able to mount/unmount exposed volumes from Nutanix ABS. 

```
sudo zypper install open-iscsi
```

## Support AFS

There is no need to install NFS client package on each worker node, because `ntnx/ntnx-csi` container image already has `nfs-client` installed for support Nutanix AFS.