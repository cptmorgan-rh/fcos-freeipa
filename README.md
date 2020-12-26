FreeIPA on Fedora CoreOS in VMware with Static IP
===========================================

## Description
------------

The goal of this repository is to provide a simple, reproducible way to deploy FreeIPA on a Fedora CoreOS server inside of VMware with a Static IP. The server is deployed with 2 systemd services. The first service clones the [freeipa-container](https://github.com/freeipa/freeipa-container) repository and then builds the image based on the latest Dockerfile. The second systemd service will run the FreeIPA container.

## Quickstart

Start by editing the `group_vars/all.yml` file:

+ Set the vCenter variables
    1. IP/Host Name of vCenter
    2. vCenter Network
    3. Datastore name
    4. Datacenter name
    5. username and passwords of vCenter Account
    6. Absoluate folder path - e.g /DataCenter/vm/Folder/
    7. VM Power state after being deployed

+ Configure your Fedora CoreOS URL and govc version.
    1. Set the Fedora CoreOS stream version. `stable` is the default

+ Configure your FreeIPA VM Settings
    1. VM and Host Name
    2. IP Addr, Gateway, Net Mask, DNS
    3. Number of CPUs
    4. Amount of Memory in MB
    5. Size of the HDD in GBs

+ Configure your FreeIPA Admin and DS Password

## Infrastructure Prerequisites

1. vSphere ESXi and vCenter 6.7 or 7.0 installed.
2. A datacenter created with a vSphere host added to it and a datastore exists that has adequate capacity.
3. Ansible (preferably latest) on the machine where this repo is cloned.
    1. Before you install Ansible, install the `epel-release`, run `yum -y install epel-release`

## USAGE

### Run Deploy Playbook
```sh
# Deploy the Lab and all components
ansible-playbook deploy-freeipa.yml
```
### deploy-aio-lab.yml Extra Variables

`skip_ova=true` - Skips downloading and deploying the OVA if previous deployed to vCenter.
`redeploy=true` - Deletes existing FreeIPA vm

### Expected Outcome

1. Necessary Linux packages installed for the installation
2. Necessary folders [bin, downloads] created
3. `govc` downloaded and extracted
4. FCOS ova downloaded to the **downloads** folder
5. FreeIPA VM is created in the designated folder and (in state of) **poweredon**

AUTHOR
------
Morgan Peterman
