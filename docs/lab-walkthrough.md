# Lab walkthrough

Summary of each build phase, in the order it was done.

## 1. TrueNAS SCALE deployment
1. Created a VM in VMware Workstation and booted the TrueNAS SCALE installer
2. Chose *Install/Upgrade*, selected the boot disk, set the admin password, rebooted
3. Opened the web UI from the VM's IP address

## 2. RAID pool
1. *Storage → Create pool*
2. Pool name, layout **RAIDZ1**, number of data disks
3. Added **one spare** disk (automatically replaces a failed disk)
4. Result: a RAID 5-equivalent pool

## 3. SMB share
1. *Credentials → Local Groups*: create group `SMB`
2. Create a user and assign it to the group
3. *Datasets → Add Dataset*, then edit permissions (read / write / execute) for the user
4. *Shares → SMB → Add*, point to the dataset
5. Test from Windows (`\\<truenas-ip>`) with the user account

## 4. NFS share
1. Create dataset, dedicated user and group
2. Grant permissions on the dataset
3. Start the NFS service, add the share
4. Test from an Ubuntu VM on the same network

## 5. iSCSI storage
1. *Shares → iSCSI → Configure*: default IQN and port, portal listening address, initiator group
2. Create the authorized user
3. Create a **zvol**, then an **extent** on it
4. Create the **target** and associate target ↔ extent (or use the wizard)
5. Test 1: add *Software iSCSI* storage in XenCenter on a Citrix XenServer VM
6. Test 2: Windows *iSCSI Initiator* → Discovery → Connect → Disk Management (online, initialize, format NTFS)

## 6. FTP
1. Dataset, user, permissions
2. Enable the FTP service, adjust settings
3. Test from a Windows machine and upload a file

## 7. ESXi and nested lab
1. Install ESXi 7 on the physical server, set static IP and DNS from the console (F2)
2. Create a **VMFS 6** datastore
3. Create two nested ESXi VMs inside it

## 8. vCenter
1. Deploy the vCenter appliance in two stages (deployment, then configuration with SSO domain)
2. Create a datacenter, add the three ESXi hosts (disable lockdown mode if needed)

## 9. Virtual networking
- **VSS**: *Networking → Virtual switches → Add standard virtual switch*, choose uplink, add a port group
- **VDS** (vCenter): *Networking → Distributed Switch → New*, choose version and uplinks, add and manage hosts, map physical adapters, create distributed port groups

## 10. Content library and VMs
1. Create a published content library on an ESXi datastore, import the Windows Server 2019 ISO
2. Create VMs: AD/DNS server, Windows 10 client, IIS web server, IIS FTP server

## 11. DNS and Active Directory
1. Install the DNS role; create forward zone and reverse zone (`192.168.112.x`)
2. Add A records, test with `nslookup`
3. Promote the server to domain controller (new forest `corp.local`)
4. Join the Windows 10 client to the domain

## 12. ESXi and vCenter with AD
- **ESXi**: *Manage → Security & Users → Authentication → Join Domain*; test with a user placed in the *ESX Admins* group
- **vCenter**: *Administration → Single Sign-On → Identity Providers* → Active Directory as LDAP server (port 389 or 636 for LDAPS); assign a role to a domain user and log in with it

## 13. Templates, clones, HA
1. Power off a Windows 10 VM → *Convert to template* → deploy new VMs from it
2. *Clone → Clone to Virtual Machine* for a one-off copy
3. Create a **cluster**, drag the three hosts in
4. *Configure → vSphere Availability → Edit → enable vSphere HA* (requires shared storage — the TrueNAS iSCSI datastore)
