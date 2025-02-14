# GlusterFS Quickstart Guide

A straightforward guide to installing, configuring, and managing GlusterFS.

---

## Table of Contents
1. [Prerequisites](#prerequisites)  
2. [Installation & Setup](#installation--setup)  
   - [Install Dependencies](#install-dependencies)  
   - [Install GlusterFS Server](#install-glusterfs-server)  
   - [Enable and Start the Service](#enable-and-start-the-service)  
3. [Cluster Configuration](#cluster-configuration)  
   - [Peer Probe](#peer-probe)  
   - [Check Peer Status](#check-peer-status)  
4. [Removing a GlusterFS Server](#removing-a-glusterfs-server)  
   - [Migrate the Brick](#migrate-the-brick)  
   - [Check Migration Status](#check-migration-status)  
   - [Remove the Brick](#remove-the-brick)  
5. [Rebalance the Volume](#rebalance-the-volume)  
   - [Start Rebalance](#start-rebalance)  
   - [Check Rebalance Status](#check-rebalance-status)  
6. [Useful Links & References](#useful-links--references)
7. [Backup & Restore](#backup--restore)  
   - [Backup](#backup)  
   - [Restore](#restore)
     
---

## Prerequisites

- **Operating System**: Ubuntu (or another Debian-based system).
- **User Privileges**: `sudo` or root access.
- **Network Connectivity**: Ensure all peers can communicate over the network.

---

## Installation & Setup

### Install Dependencies

```bash
sudo apt-get update
sudo apt-get install -y ca-certificates curl
```

## Backup & Restore

### Backup

Backup using Rsync

```
# rsync the brick folder to backup server or storage server
rsync -avz /gluster/brick1 backup-server:/backup/gluster/

# set crontab to automate the backup
0 0 * * * rsync -avz /gluster/brick1 backup-server:/backup/gluster/
```

Geo Replication Backup (Disaster Recovery GlusterFS)

```
#Create volume to drc glusterfs cluster
gluster volume geo-replication gv0 drc-server::backup-gv0 create push
#Start the volume
gluster volume geo-replication gv0 drc-server::backup-gv0 start
#Check gluster volume status
gluster volume geo-replication gv0 drc-server::drc-gv0 status

```
Full Backup GlusterFS
```
gluster volume stop gv0

tar -czvf /backup/gv0-brick1.tar.gz /gluster/brick1/
```
### Restore
```
# Restore Full Backup File GlusterFS
tar -xzvf /backup/gv0-brick1.tar.gz -C /gluster/brick1/

gluster volume start gv0
```
## Resize GlusterFS Volume
### Reduce Volume

```# Reduce Disk Volume GlusterFS
gluster volume remove-brick gv0 172.16.129.132:/gluster/brick1 start
# check status
gluster volume remove-brick gv0 172.16.129.132:/gluster/brick1 status
# remove brick 
gluster volume remove-brick gv0 172.16.129.132:/gluster/brick1 commit
# rebalance the glusterfs
gluster volume rebalance gv0 start
# check rebalance status
gluster volume rebalance gv0 status
```
