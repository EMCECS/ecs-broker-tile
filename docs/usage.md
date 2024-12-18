[Home](index.md) | [Installing](installing.md) | [Using](usage.md) | [Release Notes](release-notes.md) | [Troubleshooting](troubleshooting.md)

This topic describes how to use ECS Service Broker for VMware Tanzu after it has been installed.

## <a id='using'></a> Using ECS Service Broker for VMware Tanzu with an App

To use ECS Service Broker for VMware Tanzu with an app, follow the procedures in this section to create a service instance and bind the service instance to your app. For more information about managing service instances, see [Managing Service Instances with the cf CLI](https://techdocs.broadcom.com/us/en/vmware-tanzu/platform/tanzu-platform-for-cloud-foundry/4-0/tpcf/services-managing-services.html).

### <a id="list"></a> View the Service

After the tile is installed, `ecs-broker` and its service plans appear in your Marketplace. Run `cf marketplace` to see the service listing.

```
$ cf marketplace
Getting services from marketplace in org test / space test as admin...
OK

service            plans                             description
ecs-bucket         5gb, unlimited*                   Elastic Cloud S3 Object Storage Bucket
```

### <a id="create"></a> Create a Service Instance

Use `cf create-service` to provision a bucket.

The following example creates a `5gb` service that provisions a bucket.

```
$ cf create-service ecs-bucket 5gb my-bucket
```

Check the creation status using `cf services`. This displays a list of all your service instances. To check the status of a specific service instance, run `cf service NAME-OF-YOUR-SERVICE`.

### <a id="bind"></a> Bind the Service Instance to an App

After you create your bucket, run `cf bind-service` to bind the service to your app.

```
$ cf bind-service sample-app my-bucket
```

In tiles using broker (software) version 1.1.3 and later connected to ECS v3.3 and later, bucket policy can be applied to ECS buckets provisioned by the broker. This is enabled on binding like this:

```
$ cf bind-service sample-app my-bucket -c '{"policy": "default-total-access"}'
```

This parameter gives the binding user full control of the bucket, including the ability to set bucket policy. As of broker v1.1.3 this is the only policy that can be set via cf.
In order to apply a custom bucket policy use the binding parameters, as shown above, to grant the user permission to alter bucket policy. Then, using another method, set the bucket policy with the binding user/credentials.
Support for custom bucket policy application via cf is in progress.

### <a id="restart"></a> Restage or Restart Your App

To enable your app to access the service instance, run `cf restage` or `cf restart` to restage or restart your app.

### <a id="obtain"></a> Obtain Service Instance Access Credentials

After you bind your service instance to your app, you can find the credentials of your ECS S3 user in the environment variables of the app.

Run `cf env APP-NAME` to display environment variables. The credentials are listed under the [VCAP_SERVICES](https://techdocs.broadcom.com/us/en/vmware-tanzu/platform/tanzu-platform-for-cloud-foundry/6-0/tpcf/deploy-apps-environment-variable.html#VCAP_SERVICES) key.

```
$ cf env sample-app
Getting env variables for app sample-app in org test / space test as admin...
OK

System-Provided:
{
 "VCAP_SERVICES": {
  "ecs-bucket": [
   {
    "credentials": {
     "access_key_id": "EXAMPLE-ACCESS-KEY",
     "bucket": "ecs-cf-broker-c369db61-8382-49c7-a1d4-75e6a5a43786",
     "endpoint": "EXAMPLE-ECS-OBJECT-END-POINT-URL",
     "s3Url": "http://<access_key_id>:<secret_access_key>@<EXAMPLE-ECS-OBJECT-END-POINT-URL>/ecs-cf-broker-c369db61-8382-49c7-a1d4-75e6a5a43786",
     "secret_access_key": "EXAMPLE-SECRET-ACCESS-KEY"
    },
    "label": "ecs-bucket",
    "name": "my-bucket",
    "plan": "5gb",
    "provider": null,
    "syslog_drain_url": null,
    "tags": [
     "s3",
     "bucket"
    ],
    "volume_mounts": []

   }
  ]
 }
}
...
```

You can use the access key ID, secret access key, bucket, and region to connect to a bucket.


## <a id='deleting'></a> Delete an ECS Service Broker for VMware Tanzu Service Instance

Follow the instructions below to unbind your service instance from all apps and delete it.

<p class="note warning"><strong>WARNING:</strong> This operation cannot be undone, and all the data is lost when the service is deleted. Before deleting a service instance, you must back up the data stored in your bucket.</p>

### <a id="list2"></a> List Available Services

Run `cf service` to list your available services.

```
$ cf service

Getting services in org test / space test as admin...
OK

name           service    plan    bound apps   last operation
my-bucket      ecs-bucket 5gb     sample-app   create succeeded
```

The above example shows that `my-bucket` is bound to the `sample-app` app.

### <a id="unbind"></a> Unbind a Service Instance

Run `cf unbind` to unbind the service from your app:

```
$ cf unbind-service sample-app my-bucket
```

### <a id="delete"></a> Delete a Service Instance

Run `cf delete-service` to delete the service.

```
  $ cf delete-service my-bucket
```

Run the `cf services` command to check the deletion status.


## <a id='using'></a> Use ECS Service Broker for VMware Tanzu with an App

To use ECS Service Broker for VMware Tanzu with an app, follow the procedures in this section to create a service instance and bind the service instance to your app. For more information about managing service instances,
see [Managing Service Instances with the cf CLI](https://techdocs.broadcom.com/us/en/vmware-tanzu/platform/tanzu-platform-for-cloud-foundry/4-0/tpcf/services-managing-services.html).

### <a id="remote"></a> Connect an ECS Service to a Remote VMware Tanzu Instance

There are cases in which a single logical app is spread across multiple VMware Tanzu instances. Often in these cases there is a desire to share data between these app instances.

In the past, doing so required the developer to create "user provided services", but doing this is less than ideal, since the process is complex and VMware Tanzu has no way to know when it is safe to delete a bucket bound via a user-provided service.

The ECS service broker supports the ability to create a "remote connection" to an existing bucket, which allows developers to take advantage of the strongly-consistent geo-distribution features of ECS, and retain the VMware Tanzu experience.

Having created a bucket named `my_bucket` previously, you cannot connect to that bucket on another VMware Tanzu instance. First on the original VMware Tanzu instance, create a "remote connection" service key by running the following command:

```
$ cf create-service-key my-bucket my-bucket-key-1 -c '{"remote_connection": true}'
```

View the service key information created by running the following command:

```
$ cf service-key my-bucket my-bucket-key-1

{
 "accessKey": "12345678-abcd-2345-5678-1234abcd0987",
 "instanceId": "87654321-dcba-1234-1234-1234abcd0987",
 "secretKey": "abcd0123-4321-dcba-1f2e-1234abcd0987"
}
```

Next on the _alternate_ VMware Tanzu instance, create an service instance of the same bucket connecting remotely to the existing one. Put service key JSON as `remote_connection` value :

```
$ cf create-service ecs-bucket unlimited my-bucket-remote -c '{"remote_connection": { "accessKey": "12345678-abcd-2345-5678-1234abcd0987", "instanceId": "87654321-dcba-1234-1234-1234abcd0987", "secretKey": "abcd0123-4321-dcba-1f2e-1234abcd0987" } }'
```

Ensure that the service and plan definitions (defined in the broker catalog) are the same between the brokers on all VMware Tanzu instances.
If the catalog definitions differ between the two, the broker will return an error to the user and decline to remotely connect the service instance.
