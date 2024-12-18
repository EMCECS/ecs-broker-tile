[Home](index.md) | [Installing](installing.md) | [Using](usage.md) | [Release Notes](release-notes.md) | [Troubleshooting](troubleshooting.md)

## <a id="ver-2-3-3"></a> v2.3.3

**Release Date:** November 25, 2024

* ***This is the last release of the ECS Service Broker, no further versions will be released.***
* ***Support for the broker will end on May 25, 2025. No support will be provided after this date.***

In this release:

* Support for Tanzu Application Services version 5.x and 6.x
* Support for Ubuntu Jammy stemcell
* Upgraded dependencies to address CVEs

## <a id="ver-2-3-2"></a> v2.3.2

**Release Date:** February 23, 2024

In this release:

* Bugfixes
  - Relax verification for remote connection creation
* Upgraded dependencies to fix CVEs

## <a id="ver-2-3-1"></a> v2.3.1

**Release Date:** April 7, 2023

In this release:

* Bugfix: unbind should not fail if user or bucket does not exist
* Binary dependencies updates to address CVEs (Spring Boot v2.7.9, Spring Cloud Open Service Broker v3.6.0, logback v1.2.11, Jersey Client v2.39, slf4j 1.7.36)


## <a id="ver-2-3-0"></a> v2.3.0

**Release Date:** July 26, 2022

In this release:

* TAS context values as bucket tags
* ADO read-only support for new buckets, and bucket ADO changes on plan change
* Binary dependencies updates to address CVEs (Spring Boot 2.7.2, Guava 31.1, Logback 1.2.9, Log4j 2.17.2)


## <a id="ver-2-2-1"></a> v2.2.1

**Release Date:** April 25, 2022

In this release:

* Added support for AWS signature V4 mode
* Binary dependencies update (Spring Boot 2.6.7)


## <a id="ver-2-2-0"></a> v2.2.0

**Release Date:** March 21, 2022

In this release:

* Bucket expiration - service and plan settings
* Application binary version update to 2.2.0: dependencies version updates
* Runtime update to JRE 11

## <a id="ver-2-1-4"></a> v2.1.4

**Release Date:** December 17, 2021

In this release:

* Hotfix: Dependencies update to avoid log4jShell vulnerability

## <a id="ver-2-1-3"></a> v2.1.3

**Release Date:** August 26, 2021

In this release:

* Bugfix: S3 testing logged warning when no issues found
* Additional log statements to ease S3 connection debug

## <a id="ver-2-1-2"></a> v2.1.2

**Release Date:** July 02, 2021

In this release:

* Bugfix: remote-instance bindings failed with NPE
* Bugfix: custom name prefix not included in binding credentials


## <a id="ver-2-1-1"></a> v2.1.1

**Release Date:** March 12, 2021

In this release:

* Added: Bucket custom tags and search metadata configuration in Catalog Service settings
* Bugfix: S3 path style access was not applied to bucket bindings


## <a id="ver-2-1-0"></a> v2.1.0

**Release Date:** March 2, 2021

In this release:

* Added: Namespace, replication group and base URLs settings in services and plans
* Added: S3 path style access control in broker settings
* Application binary version update to 2.1.0:
* Added: Bucket search metadata config support (via env)
  * Added: Bucket custom tags config support (via env)
  * Added: Default retention period setting support
  * Added: REST API for instances and bindings listing
  * Added: UID in instance binding credentials for file enabled buckets
  * Dependencies version updates


## <a id="ver-2-0-5"></a> v2.0.5

**Release Date:** October 7, 2020

In this release:

* Added: TAS 2.10.x support
* Added: S3 object endpoint credentials validation on application startup
* Fixed: namespace fails to create when bucket quota input is empty


## <a id="ver-2-0-4"></a> v2.0.4

**Release Date:** September 16, 2020

Fix in this release:

* fix: application jar not updated, namespace title not added to binding credentials


## <a id="ver-2-0-3"></a> v2.0.3

**Release Date:** September 15, 2020

Fixes in this release:

* fix services description: service icon, description and external links missing in Apps Manager marketplace.
* fix namespace binding credentials: no namespace title in binding credentials


## <a id="ver-2-0-2"></a> v2.0.2

**Release Date:** September 1, 2020

Fixes in this release:

* fix error messages: description missing from response body, empty brackets displayed in Apps Manager UI.
* fix upgrades from 2.0.0: errand might fail on PCF 2.8


## <a id="ver-2-0-1"></a> v2.0.1

**Release Date:** August 21, 2020

Features added in this release:

* Added configuration flag to enable HTTPS when using base url to generate object endpoint address and S3 URLs for bound applications
* Optional name prefix parameter for services and bindings: a prefix to be added after broker prefix; generated name will have form of "broker prefix"-"optional prefix"-"GUID"

Fixes and updates:

* fix upgrades from 1.2.4: errand failed to registered broker due to installation to wrong org and space.
* fix non-existent objects delete: requests failed when object cannot be found.
* fix exception thrown on namespace binding when no Base URL configured for broker or provided as optional parameter
* dependency updates: Spring Boot 2.2.9, Spring Cloud Open Service Broker 3.1.2


## <a id="ver-2-0-0"></a> v2.0.0

**Release Date:** June 12, 2020

Features included in this release:

* Input field for a plan price currency.
* Сonfigurable reclamation policies for buckets during service instance deletion ("delete", "detach" or "fail")

## <a id="ver-1-2-4"></a> v1.2.4

**Release Date:** October 21, 2019

Fix included in this release:

* Namespace binding now working.

## <a id="ver-1-2-3"></a> v1.2.3

**Release Date:** June 6, 2019

Fix included in this release:

* Bucket policy is now applied explicitly on bind instead of implicitly. See docs.

## <a id="ver-1-2-2"></a> v1.2.2

**Release Date:** May 13, 2019

Fix included in this release:

* Fixes issue where renaming fails and creates duplicate broker/app on upgrade.

## <a id="ver-1-2-1"></a> v1.2.1

**Release Date:** April 9, 2019

Feature included in this release:

* Now supports bucket policies.

## <a id="ver-1-2-0"></a> v1.2.0

**Release Date:** February 15, 2019

Fix included in this release:

* Fixes the issue where an unwanted org was created during upgrade.
This issue caused routing problems and bad upgrades.

Feature included in this release:

* Upgrades the stemcell to Ubuntu Xenial.

## <a id="ver-1-1-1"></a> v1.1.1

**Release Date:** October 2, 2018

Fix included in this release:

* Fixes thrown exception during service plan update


## <a id="ver-1-1-0"></a> v1.1.0

**Release Date:** August 23, 2018

Fix included in this release:

* Failure to mount via NFS without export directory specified

Features included in this release:

* Support host-based addressing URL in service binding credentials
* Support multiple VMware Tanzu instances to address the same bucket/namespace services


## <a id="ver-1-0-2"></a> v1.0.2

**Release Date:** October 30, 2017

Fixes included in this release:

* Fixes for tile support for service tags and plan bullets
* Bump memory requirement for app to 1&nbsp;GB


## <a id="ver-1-0-1"></a> v1.0.1

**Release Date:** October 23, 2017

Fixes included in this release:

* Proper serialization of the `broker-api-version` property, as a string
* Enables service-access for all services

Features included in this release:

* Improves tile form layout and descriptions
* Supports administrator configured catalog services
* Uses CredHub for service broker credentials


## <a id="ver-1-0-0"></a> v1.0.0

**Release Date:** Aug 24, 2017

Features included in this release:

* On-Demand service instance provisioning
* Requires stemcell 3312.12
* Supports VMware Tanzu v1.10.x and later
