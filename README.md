# csi-plugin

This repository contains  Nutanix CSI driver deployment yamls for different OS
and kubernetes distributions. The repository also contains example usage for
the CSI driver.

## Important notice
Please note that with v2.2.0, Nutanix CSI driver has changed format of driver name from com.nutanix.csi to csi.nutanix.com. All deployment yamls uses this new driver name format. However, if you are upgrading the CSI driver then you should continue to use old driver name com.nutanix.csi. Existing PVC/PV will not work with the new driver name. Please search and replace csi.nutanix.com to com.nutanix.csi before applying the new depoyment yamls.

## Nutanix CSI driver v2.4.1 documentation
https://portal.nutanix.com/page/documents/details?targetId=CSI-Volume-Driver-v2_4_1:CSI-Volume-Driver-v2_4_1

This release brings in Volume metrics and CSI operations metrics support.

## Nutanix CSI driver v2.3.1 documentation
https://portal.nutanix.com/page/documents/details?targetId=CSI-Volume-Driver-v2_3:CSI-Volume-Driver-v2_3

This release provides a common deployment yamls for all linux flavors (Centos, Ubuntu, RHCOS etc)

## Nutanix CSI driver v2.2.0 documentation
https://portal.nutanix.com/page/documents/details?targetId=CSI-Volume-Driver-v2_2:CSI-Volume-Driver-v2_2

New Features:
1. LVM Volume supporting multi vdisks volume group
2. NFS dynamic share provisioning
3. iSCSI Auto CHAP Authentication

Quick Start Guide: https://github.com/nutanix/csi-plugin/blob/master/csi-v2.2.0.md

## Nutanix CSI driver v2.1.0 documentation
https://portal.nutanix.com/page/documents/details?targetId=CSI-Volume-Driver-v2_1:CSI-Volume-Driver-v2_1

New feature:
IP Address Whitelisting
 
## Nutanix CSI driver v2.0.0 documentation
https://portal.nutanix.com/page/documents/details?targetId=CSI-Volume-Driver-v2_0:CSI-Volume-Driver-v2_0

New features:
1. Volume clone
2. Volume snapshot and Restore

Quick Start Guide: https://github.com/nutanix/csi-plugin/blob/master/csi-v2.0.0.md

## Nutanix CSI driver v1.1.0 documentation
https://portal.nutanix.com/#/page/docs/details?targetId=CSI-Volume-Driver-v1_1:CSI-Volume-Driver-v1_1

New features:
1. Raw Block Volume
2. Volume Expansion
3. CSIDriver Object
4. Liveness Probe

## Nutanix CSI driver v1.0.1 documentation:
https://portal.nutanix.com/#/page/docs/details?targetId=CSI-Volume-Driver-v10:CSI-Volume-Driver-v10
Please use Tag v1.0.1 to download deployment yamls compatible to v1.0.1. 

