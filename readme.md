ceph health detail
ceph -s
ceph osd pool ls
ceph ods pool ls detail
ceph osd pool get kubernetes size
ceph osd pool get kubernetes min_size
ceph osd pool stats kubernetes
ceph osd tree
ceph osd df

To list disks attached on the ceph system
 ceph orch device ls

 To add a disk to new node. First add the node on the disk. for example a 50 GB disk. Then run below command
 ceph orch device ls --refresh
 ceph orch apply osd --all-available-devices
  ceph orch device ls

  Now fetching the ceph details to configure csi driver on OCP.

  ceph fsid
  ceph mon dump | awk '/mon\./{print $2}'
  ceph auth get-or-create client.kubernetes \
  mon 'profile rbd' osd 'profile rbd pool=kubernetes' mgr 'profile rbd pool=kubernetes' \
  -o ceph.client.kubernetes.keyring
  awk '/key =/{print $3}' ceph.client.kubernetes.keyring
