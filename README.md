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

*NOTE*: This repository is a work in progress. Do not use yet.

