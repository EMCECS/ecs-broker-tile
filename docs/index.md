[Home](index.md) | [Installing](installing.md) | [Using](usage.md) | [Release Notes](release-notes.md) | [Troubleshooting](troubleshooting.md)

This documentation describes ECS Service Broker for VMware Tanzu.

## <a id="overview"></a> Overview

ECS Service Broker for VMware Tanzu registers a service broker on VMware Tanzu and exposes its service plans on the Marketplace.
Developers can provision buckets by creating instances of service plans using Apps Manager or the cf Command Line Interface (CLI) tool.

## <a id='features'></a> Key Features

With ECS Service Broker for VMware Tanzu, you can do the following:

* Create and delete object storage buckets.
* Create and delete object storage namespaces.
* Bind one or more Cloud Foundry apps to a bucket or namespace, with unique credentials and permissions for each app.
* Support quota-enforced plans for buckets to limit the amount of capacity.
* Support encryption and retention of namespaces.
* Change plans of an existing bucket.
* Browse Cloud Foundry instance and binding metadata through an internal bucket.
* Specify an ECS namespace and replication group for provisioning.
* Assign custom tags and configure search metadata for buckets.
* Provide a string prefix for bucket and user names.
* Support a self-signed SSL certificate for the ECS management API.
* Support file system mounts of file access enabled buckets via NFS.
* Configure offered services and plans through Ops Manager Tile.
* Support for shared buckets across multiple VMware Tanzu instances.

## <a id="snapshot"></a>Product Snapshot

| Element      | Details                            |
|:-------------|:-----------------------------------|
| Tile Version | 2.3.3                              |
| Release Date | November 25, 2024                  |
| Software component version | 2.3.3                              |
| Compatible Ops Manager version(s) | v3.0.x, v2.10.x            |
| Compatible Tanzu Application Service version(s) | v6.0.x, v5.0.x, v4.0.x     |
| BOSH stemcell version | Ubuntu Jammy 1.506                   |
| IaaS support | AWS, Azure, OpenStack, and vSphere |
| IPsec support? | No                                 |

## <a id="reqs"></a> Requirements

ECS Service Broker for VMware Tanzu has the following requirements:

+ [Tanzu Application Service](https://support.broadcom.com/group/ecx/productdownloads?subfamily=VMware%20Tanzu%20Application%20Service%20for%20VMs)
