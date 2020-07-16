# SLES 15SP1

Support Nutanix CSI driver running on SUSE Linux Enterprise Server 15SP1 (SLES 15SP1). 

## Support ABS

Install iSCSI Initiator package on each worker node for being able to mount/unmount exposed volumes from Nutanix ABS. 

```
sudo zypper install open-iscsi
```

## Support AFS

There is no need to install NFS client package on each worker node, because `ntnx/ntnx-csi` container image already has `nfs-client` installed for support Nutanix AFS.

## General steps to configure Nutanix volumes CSI:
1. `kubectl apply -f ntnx-csi-psp.yaml`
2. `kubectl apply -f ntnx-csi-rbac.yaml`
* Verify:  
	* `kubectl get serviceaccounts -n kube-system | grep csi`
	* `kubectl get clusterrole -n kube-system | egrep "csi|runner"`
	* `kubectl get clusterrolebinding -n kube-system | grep csi`
3. `kubectl apply -f ntnx-csi-node.yaml`
* Verify: `kubectl get daemonset -n kube-system | grep csi`
4. `kubectl apply -f ntnx-csi-provisioner.yaml`
* Verify: `kubectl get statefulset -n kube-system | grep csi`
5. `kubectl apply -f csi-driver.yaml`
6. Set the PRISM_LOGIN variable with the base64 hash of the Prism login information in the form of "<PrismIP>:<port, normally 9440>:<username>:<password>": 
* I.e. `export PRISM_LOGIN=$(echo -n "10.10.10.10:9440:admin:p@ssw0rd" | base64)`
7. Update the ntnx-secret.yaml file with the login hash: `sed  -i "s/key:.*/key: ${PRISM_LOGIN}/" ntnx-secret.yaml`
8. `kubectl apply -f ntnx-secret.yaml`
* Verify: `kubectl get secret -n kube-system | grep ntnx-secret`
9: Update the ntnx-volume-storage-class.yaml file to match your environment (Hint: Comments in the file should help find the relevant information)
10. `kubectl apply -f ntnx-volume-storage-class.yaml`
* Verify: `kubectl get storageclass`
	* Take note if the acs-abs storageClass is the default
11. Test that a PV/PVC can be created via the new storageClas (Hint: Comment out the "storageClassName: acs-abs" line to test the default storageClass): `kubectl apply -f test-pvc.yaml`
* Verify: `kubectl get pvc`
12. After the PVC shows a STATUS of "Bound", create a test pod to mount the PVC: `kubectl apply -f test-pod.yaml`
* Verify: `kubectl get pods`
13. After the test-pod show READY "1/1" and STATUS "Running", verify the pod has mounted the PVC: `kubectl exec -it test-pod -- mount | grep test-vol`
* Verify: The output should include "/mnt/test-vol type ext4"
14. To delete the test-pod and test-pvc: `kubectl delete -f test-pvc.yaml; kubectl delete -f test-pod.yaml`
