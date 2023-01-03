Ansible Playbook to migrate RHV VMs into RHOSP

Prerequisites:
 
- ovirt-img package

- Tested with Ansible 2.9

- Access to OSP and RHV API endpoints

- OSP and RHV credentials


The playbook:

- Gets VM name, OSP flavor and OSP project name as variable


- The playbook check if there is a single disk or multiple disks attached to the VM.


- Shuts down the VMs and uses ovirt-img tool to download the disk images in raw format (Red Hat does not support qcow format when the OSP backend is RHCS)


- Uploads the images to glance and starts the instances at OSP with using cinder volumes backed by glance images.


- It was assumed that RHV VMs are using either UUID or LVM for the disk partitions at fstab. If not, a manual intervention (editing fstab with UUID of the disks) is required once the Instance boots up at OSP.


- If the VMs at RHV are using consistent device naming(ex ens*)  and the order was changed due to removing/adding interfaces, a manual intervention is required (mapping to the correct interface device) once the instance becomes up at OSP.
