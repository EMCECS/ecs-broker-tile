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

| Element      | Details                                                                      |
|:-------------|:-----------------------------------------------------------------------------|
| Tile Version | 2.3.2                                                                        |
| Release Date | February 23, 2024                                                            |
| Software component version | 2.3.2                                                                        |
| Compatible Ops Manager version(s) | v3.0.x, v2.10.x, v2.9.x                                    |
| Compatible Tanzu Application Service version(s) | v4.0.x, v3.0.x, v2.13.x, v2.12.x, v2.11.x, v2.10.x, v2.9.x |
| BOSH stemcell version | Ubuntu Xenial 621                                                            |
| IaaS support | AWS, Azure, OpenStack, and vSphere                                           |
| IPsec support? | No                                                                           |

## <a id="reqs"></a> Requirements

ECS Service Broker for VMware Tanzu has the following requirements:

+ [Tanzu Application Service](https://network.pivotal.io/products/elastic-runtime)


## <a id="feedback"></a> Feedback

Report bugs, make feature requests or ask questions on the [VMware Tanzu Feedback](mailto:pivotal-cf-feedback@pivotal.io) list,
or send an email to [ECS Service Broker Support](mailto:ecs.open.service.broker@dell.com).
