Ceph playground with a 3-node cluster
=====================================

### ceph-deploy ###
```
sudo vi /etc/hosts
172.16.16.16    ceph-deploy
172.16.17.1	mon1
172.16.18.1	osd1
172.16.18.2	osd2
```

### On each node ###
```
sudo apt-get install -y python ntp
sudo adduser bq
echo "bq ALL = (root) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/bq
sudo chmod 0440 /etc/sudoers.d/bq
su bq
```

### ceph-deploy ###
```
ssh-keygen
ssh-copy-id bq@mon1
ssh-copy-id bq@osd1
ssh-copy-id bq@osd2
vi ~/.ssh/config
Host mon1
   Hostname mon1
   User bq
Host osd1
   Hostname osd1
   User bq
Host osd2
   Hostname osd2
   User bq
```

### ceph-deploy ###
```
mkdir my-cluster
cd my-cluster
ceph-deploy new mon1
vi ceph.conf
osd pool default size = 2
public network = 172.16.0.0/12
ceph-deploy install --repo-url https://mirrors.aliyun.com/ceph/debian-jewel --gpg-url https://mirrors.aliyun.com/ceph/keys/release.asc ceph-deploy mon1 osd1 osd2
```
