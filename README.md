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

### Restore
```bash
# migrate
gluster volume remove-brick gv0 172.16.129.132:/gluster/brick1 start
# check status
gluster volume remove-brick gv0 172.16.129.132:/gluster/brick1 status
# remove brick 
gluster volume remove-brick gv0 172.16.129.132:/gluster/brick1 commit
# rebalance the glusterfs
gluster volume rebalance gv0 start
# check rebalance status
gluster volume rebalance gv0 status
