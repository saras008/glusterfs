# glusterfs

sudo apt-get install ca-certificates curl

sudo apt update && sudo apt install -y glusterfs-server

sudo systemctl enable glusterd

sudo systemctl start glusterd

sudo gluster peer probe 172.16.129.135

sudo gluster peer status

## Remove GlusterFS Server
#migrate
gluster volume remove-brick gv0 172.16.129.132:/gluster/brick1 start

#check status
gluster volume remove-brick gv0 172.16.129.132:/gluster/brick1 status

#remove brick 
gluster volume remove-brick gv0 172.16.129.132:/gluster/brick1 commit

#rebalance the glusterfs
gluster volume rebalance gv0 start

#check rebalance status
gluster volume rebalance gv0 status
