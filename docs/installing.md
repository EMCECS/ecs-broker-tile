[Home](index.md) | [Installing](installing.md) | [Using](usage.md) | [Release Notes](release-notes.md) | [Troubleshooting](troubleshooting.md)

This topic describes how to install and configure ECS Service Broker for VMware Tanzu.


## <a id='install'></a> Install and Configure ECS Service Broker for VMware Tanzu

The ECS Service Broker installs as a single VMware Tanzu-deployed application, which makes API calls to an externally-hosted Dell EMC ECS installation. The broker uses a combination of both the ECS `management` API (which typically runs on port `4443` on ECS) and the S3 API (which runs on ports `9020`/`HTTP` and `9021`/`HTTPS`). If you do not yet have access to an ECS environment, you have two options:

* Install the [ECS Community Edition](https://github.com/EMCECS/ECS-CommunityEdition) Docker-based install.
* Use the publicly available [ECS Test Drive](https://portal.ecstestdrive.com).

To install the service broker, you must configure the broker application to connect to the ECS management API. If desired, you may also customize the services and plans offered in the VMware Tanzu marketplace with additional pages in the Tile interface.

To start running the ECS broker, do the following:

1. Download the product file from [Broadcom Support portal](https://support.broadcom.com/group/ecx/productdownloads?subfamily=ECS%20Service%20Broker%20for%20VMware%20Tanzu).

1. Navigate to the Ops Manager Installation Dashboard and click **Import a Product** to upload the product file.

1. Under the **Import a Product** button, click **+** next to the version number of ECS Service Broker for VMware Tanzu. This adds the tile to your staging area.

1. Click the newly added **ECS Service Broker for VMware Tanzu** tile.


## <a id='install'></a> Configure ECS Service Broker for VMware Tanzu

1. Navigate to **Assign AZs and Networks** and confirm that the default Availability Zones and Network fields are correct.

1. Click **Save** if any changes have been made.

1. Navigate to **Dell EMC ECS Connectivity**.

1. For **ECS Management Endpoint**, enter the URI/endpoint for the ECS HTTPS management API. This typically runs on port `4443` of the ECS. For ECS Test Drive users, see the **ECS Management** page.

1. For **Replication Group**, enter the name of the ECS replication group to be used for created buckets. For ECS Test Drive users, this should be `ecstestdrivegeo`.

1. For **Namespace**, enter the name of the ECS namespace to be used for created buckets and users.

1. For **ECS Admin Username**, enter the name of the ECS Management API user. In ECS terminology, this is a Management User (not an Object User), which should configured as either a Namespace Administrator or System Administrator.

1. For **ECS Admin Password**, enter the ECS Management API password.

1. (Optional) For **ECS Base URL**, enter the name of the ECS configured base URL that should be used with bucket credentials. If no value is entered, the broker will attempt to discover a default value. If this feature is enabled, ensure that the management user has System Monitor access on the ECS.

1. (Optional) If **ECS Base URL** is entered and you wish to enable SSL communications with object endpoint, set **Use HTTPS** flag - with that, broker object endpoint and application binding URLs will use HTTPS schema and 9021 port

1. Specify whether the ECS system has a certificate installed, which is signed by an available trust authority. This may not be available for development environments, and is not the case for self-signed certificates.

1. If the installed ECS certificate is not signed by a trust authority, complete the **ECS Management Certificate** field by entering the ECS certificate.

1. To overload a value determined from the **Base URL**, or if no Base URL was provided, complete the **ECS Object Endpoint** field by entering the URI/endpoint for the ECS S3 API.

1. Click **Save**.

1. Navigate to **Service Broker Settings**.

1. (Optional) For **Broker Prefix**, enter a string used to prefix broker-created buckets and users. For ECS Test Drive users, use your Namespace value here to ensure that there are no username conflicts between public users.

1. (Optional) For **Repository Endpoint**, enter the URI/endpoint for the ECS S3 API that should be used for persisting broker metadata. This defaults to the object endpoint or base URL.

1. (Optional) For **Repository User**, enter the name of the user that should be created or used for managing broker metadata.

1. (Optional) For **Repository Bucket**, enter the name of the bucket that should be created or used for managing broker metadata.

1. Click **Save**.

1. Navigate to **Catalog Service 1**.

1. Review settings for catalog service and plans. These settings define the services available in the VMware Tanzu marketplace. If any changes are made, click **Save**.

1. (Optional) Navigate to **Catalog Service 2**.

1. (Optional) Enable Catalog Service 2. Review service settings and enter Default Bucket Quota value, if a Namespace type is selected. Click **Save**.

1. Review the remaining catalog services. Services 2, 3, 4 and 5 are disabled by default, but available for customization.

   <p class='note'><strong>Note:</strong> File-enabled buckets and Namespace services will not function on ECS Test Drive.</p>

1. For **Enable Global access to all Services and Plans**, navigate to **Service Access** and check the checkbox to open up access to all service plans across all orgs and spaces.

1. Click **Save**

1. Return to the Ops Manager Installation Dashboard and click **Apply Changes**.
