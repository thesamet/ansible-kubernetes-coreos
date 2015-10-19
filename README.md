Set up an Amazing CoreOS based Kubernetes Cluster on AWS through Ansible
========================================================================

The idea in using Ansible rather than CloudFormation is that it will not fill
your production AWS account with all sort of security groups, VPCs, IAM roles
and what not that you can not control.

This solution is offering a different approach.  You start a bunch of machines
and through the Ansible inventory you designate a role to them: etcd,
kubernetes master or kubernetes minion.

Other notable features:

- TLS authentication between Kubernetes components.
- AWS cloud provider support.
- DNS add-on

Running
-------
1. Customize `vars-example.yaml`

2. Create an inventory file with four groups:

- `[etcd]`: nodes that will be set up as an auxiliary etcd cluster to serve
  the kubernetes cluster.
- `[master]`: contains a single node which will be the Kubernetes master.
- `[minions]`: one or more minion nodes.
- `[coreos]`: union of all the above CoreOS machines (so they can be
  bootstrapped):
 ```
[coreos:children]
master
etcd
minions
  ```

3. Run:
```
$ ansible-playbook -i ./inventory  -e @/path/to/customized-vars.yaml provision.yaml
```

4. Then ssh to your master, and you should be able to start exploring:

```
$ /opt/local/bin/kubectl get pds

$ /opt/local/bin/kubectl get nodes
```
