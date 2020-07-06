# SLES 15SP1

Support Nutanix CSI driver running on SUSE Linux Enterprise Server 15SP1 (SLES 15SP1). 

## Support ABS

Install iSCSI Initiator package on each worker node for being able to mount/unmount exposed volumes from Nutanix ABS. 

```
sudo zypper install open-iscsi
```

## Support AFS

There is no need to install NFS client package on each worker node, because `ntnx/ntnx-csi` container image already has `nfs-client` installed for support Nutanix AFS.

## Apply the files in the following order: 
1. ntnx-csi-psp.yaml
2. ntnx-csi-rbac.yaml
* Verify: 
** `kubectl get serviceaccounts -n kube-system | grep csi`
** `kubectl get clusterrole -n kube-system | egrep "csi|runner"`
** `kubectl get clusterrolebinding -n kube-system | grep csi`
3. ntnx-csi-node.yaml 
* Verify: `kubectl get daemonset -n kube-system | grep csi`
4. ntnx-csi-provisioner.yaml
* Verify: `kubectl get statefulset -n kube-system | grep csi`
5. csi-driver.yaml
6. ntnx-secret.yaml
* Verify: `kubectl get secret -n kube-system | grep ntnx`
7. ntnx-volume-storage-class.yaml
* Verify: `kubectl get storageclass`

