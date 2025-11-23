To add the cluster to Openshift first created RBD and list the RBD device
```bash
ceph osd pool create rbd 128 128
ceph osd lspools
```
To add it to openshift cluster run below python script which can be fetched from Openshift and save it to a JSON file. We are providing the rbd pool name which was created with first `osd pool create` command
```bash
python3 ceph-exporter.py --rbd-data-pool-name rbd > rbd.json
```
Some ceph commands
```bash
ceph health detail
ceph -s
ceph osd pool ls
ceph ods pool ls detail
ceph osd pool get kubernetes size
ceph osd pool get kubernetes min_size
ceph osd pool stats kubernetes
ceph osd tree
ceph osd df
```
To list disks attached on the ceph system
```bash
 ceph orch device ls
```
 To add a disk to new node. First add the node on the disk. for example a 50 GB disk. Then run below command
```bash
ceph orch device ls --refresh
ceph orch apply osd --all-available-devices
ceph orch device ls
```

  Now fetching the ceph details to configure csi driver on OCP.
```bash
  ceph fsid
  ceph mon dump | awk '/mon\./{print $2}'
  ceph auth get-or-create client.kubernetes \
  mon 'profile rbd' osd 'profile rbd pool=kubernetes' mgr 'profile rbd pool=kubernetes' \
  -o ceph.client.kubernetes.keyring
  awk '/key =/{print $3}' ceph.client.kubernetes.keyring
```
