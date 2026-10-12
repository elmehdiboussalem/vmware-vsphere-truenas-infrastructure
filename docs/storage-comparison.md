# NAS solution comparison

| Criterion | OpenMediaVault | FreeNAS / TrueNAS | OpenFiler | NAS4Free |
|---|---|---|---|---|
| Base OS | Debian | FreeBSD | FreeBSD | FreeBSD |
| File systems | EXT2/3/4, XFS, JFS, NTFS, FAT32 | OpenZFS | NFS | OpenZFS |
| SSH | Yes | Yes | Yes | Yes |
| Active Directory sync | No | Yes | Yes | Yes |
| Open source | Yes | Yes | Yes | Yes |
| Development languages | Shell, PHP, JavaScript | Python | Python | Python |

*Table reproduced from the internship report.*

**Decision:** TrueNAS — ZFS (snapshots, pools, replication), Active Directory integration, and SMB / NFS / iSCSI support. **TrueNAS SCALE** (Debian-based) was the edition used.

## SCALE vs CORE

- **CORE**: evolution of FreeNAS, FreeBSD-based, aimed at individuals and small businesses
- **SCALE**: Debian Linux-based, scale-out capabilities, containers and Kubernetes applications
