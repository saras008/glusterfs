# glusterfs

sudo apt-get install ca-certificates curl

sudo apt update && sudo apt install -y glusterfs-server

sudo systemctl enable glusterd

sudo systemctl start glusterd

sudo gluster peer probe 172.16.129.135

sudo gluster peer status
