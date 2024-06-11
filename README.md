# NFS client configuration: ansible role

## Description

You can use this role to install and config nfs client.
The role was tested with RedHat.

It has two options:
  - automount
    It helps mouunt and unmount NFS on-demand.
  - entry in fsttab file
    Standard way to mount file systems permanently.

## Avaliable variable

It has three types of variable.
  - required
  - default
  - permanent

### Required
You MUST set these variables. The role does not work without it!:

The main thing is to define NFS server with it's options:
```
nfs_servers: 
- ip: 192.168.231.231
  fs:
  - path: /opt/server
    mount_point: /export
    mount_options: "rw,rsize=8192,wsize=8192"

In this dictionary <mount_options> is optional, defautl walue is:

client_mount_options: "rw,rsize=8192,wsize=8192"
```

$${\color{red}Attention!}$$

When you add mount point in case of autofs, it have to be a relative path!!!

### Default

You can change them if it nessesary:
```
nfs_mount_type: 'fstab'
client_mount_options: "rw 0 0"
state: present
timeout: 300
autofs_main_dir: /nfs
```
- [ ] nfs_mount_type:
    It has two options:
    - fstab - for permanent mount FS in your system
    - autofs - mount FS on-demand

- [ ] client_mount_options:
    it has been mentioned above

- [ ] state:
    It has two optiosn:
    - present - to install and config NFS client services
    - absent - to remove services

### Permanent

Almost it is vars with packages names to install with different conditions.

```
rhel_packages_list:
  - nfs-utils
debian_packages_list:
  - nfs-common
nfs3_packages:
  - rpcbind
autofs:
  - autofs

These are main files for autofs.
```
autofs_files:
  - auto.master
  - auto.nfs
```
