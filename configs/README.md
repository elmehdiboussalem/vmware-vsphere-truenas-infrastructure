# Configurations

This lab is mostly GUI-driven (TrueNAS web UI, vSphere Client), so there is little text configuration. Put here, as plain files, anything reproducible:

| File | Content |
|---|---|
| `dns-zones.md` | Forward zone `zone-directe.corp.local` and reverse zone `192.168.112.x`, with the list of A records |
| `truenas-shares.md` | Dataset names, share names, permissions model (users and groups only — **no passwords**) |
| `network-plan.md` | IP plan of ESXi hosts, vCenter, TrueNAS, AD/DNS |

Do not commit passwords, API tokens or exported certificates.
