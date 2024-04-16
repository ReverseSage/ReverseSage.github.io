---
layout: post
title: "Build your kubernetes cluster using K3S on linux"
categories: [MLOPS]
tags: ["cluster", "Kubernetes","K3S"]     # TAG names should always be lowercase
image: /assets/images/kubernetes.png
  alt: Kubernetes cluster image.
---


## Naming convention

We will be using the following naming (official documentation's naming) just to be clear and not get confused

- **Server**: means control-plane / master-node.
- **Agent**: means worker / slave.
- **Node**: Could be your virtual machine (VM) or a physical server.

## Installation

As mentioned in the [home page](https://k3s.io/) for k3s the installation is pretty easy

just run the following to install node as a **server**

```bash
curl -sfL https://get.k3s.io | sh -
```

if you want to install agents (of course, otherwise it won't be a cluster :) ) you will need to get your join token, just run the following command on your **server**:

```bash
sudo cat /var/lib/rancher/k3s/server/node-token
```

and to install node as an **agent** you can run 

```bash
curl -sfL https://get.k3s.io | K3S_URL=https://<myserver>:6443 K3S_TOKEN=<mynodetoken> sh -
```


## Uninstallation


>  Uninstalling K3s deletes the local cluster data, configuration, and all of the scripts and CLI tools. It does not remove any data from external datastores, or created by pods using external Kubernetes storage volumes.
{: .prompt-warning }

If you installed K3s using the installation script, a script to uninstall K3s was generated during installation.

If you are planning on rejoining a node to an existing cluster after uninstalling and reinstalling, be sure to delete the node from the cluster to ensure that the node password secret is removed. See the [Node Registration](https://docs.k3s.io/architecture#how-agent-node-registration-works) documentation for more information.

### Uninstalling Server

To uninstall K3s from a server node, run:

```bash
/usr/local/bin/k3s-uninstall.sh
```

### Uninstalling Agent

To uninstall K3s from an agent node, run:

```bash
/usr/local/bin/k3s-agent-uninstall.sh
```
