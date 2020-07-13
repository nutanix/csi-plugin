Quick start guide

# Volume Clone

Minimum k8s version required : v1.16

Volume cloning allows users to create a new pvc using an existing pvc. This allows users to make a new pvc containing the data of the given existing pvc and mount it in the k8s cluster. Users can then use the newly created pvc in their applications. 

The feature adds support for specifying an existing pvc name which the user wants to clone in the dataSource field of pvc creation yaml file. 

Please refer to example/ABS/claim3-pvc-clone.yaml for an example.

# Volume Snapshot and Restore

Minimum k8s version required : v1.17

Volume Snapshot allows users to create snapshots of the existing pvc in the kubernetes cluster. The snapshot is created and added as a VolumeSnapshot in the kubernetes cluster. The user can further use these snapshots as a source for creating a new pvc containing the data stored in the snapshot. VolumeSnapshots are read-only and hence a user creates the snapshot at a certain point in time and can create a new pvc using the snapshot at any point of time in future.

The feature adds support for specifying an existing VolumeSnapshot name in the dataSource field of pvc creation yaml file.

## Additional steps to enable volume snapshot:
### Install Snapshot Beta CRDs:
kubectl create -f crd
### Install Common Snapshot Controller:
kubectl create -f snapshot-controller-rbac.yaml -f snapshot-controller-setup.yaml

## Volume Snapshot Class
Just like StorageClass provides a way for administrators to describe the classes of storage they offer when provisioning a volume, VolumeSnapshotClass provides a way to describe the classes of storage when provisioning a volume snapshot.

Please refer to example/ABS/volume-snapshot-class.yaml for an example.

## Creating a snapshot
Please refer to example/ABS/snapshot1.yaml for an example.

## Creating a PVC using snapshot as a source
Please refer to example/ABS/claim2-snapshot-restore.yaml for an example.

