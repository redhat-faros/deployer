# Project Faros [![Docker Repository on Quay](https://quay.io/repository/faros/cluster-manager/status "Docker Repository on Quay")](https://quay.io/repository/faros/cluster-manager)

Project Faros is a reference implimentation of Red Hat OpenShift 4 on small,
bare-metal clusters. The project includes reference architectures and automated
deployment tools. We are looking to bring OpenShift everywhere, even to the
edge.

## Installation

Please follow [these instructions](./docs/prereqs.md) to ensure all of the
prerequisites are met and to install the Faros cluster manager.

## Cluster Deployment

Run the following commands from your bastion node:

```bash
# Launch the interactive cluster configuration TUI
farosctl config

# Create the required virtual infrastructure
# (bootstrap and virtual bastion app node)
farosctl create machines

# Configure network infrastructure (DNS and DHCP)
farosctl create network

# Reboot out-of-band controllers to ensure they pick up their assigned IPs.

# Create the cluster load balancer
farosctl create load-balancer

# Create the installation source and config repositories
farosctl create install-repos

# Create the OpenShift cluster
farosctl create cluster
```

That's it!

## Connecting the the Cluster

During install, cockpit is installed on the bastion node and hosted on port
9090. Check that out [here](http://bastion:9090). Log in with the standard user
account. This interface can be used to check virtual machines and get a
terminal session on the server. There will also be a Faros tab with helpful
links to various cluster resources.

The farosctl command can be used to connect to the cluster as well.

```bash
farosctl oc get nodes
```

Any of the `oc` commands can be executed this way. They will be run as the
default `kubeadmin` user.
