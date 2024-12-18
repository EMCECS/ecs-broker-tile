# EMC ECS Service Broker PCF Tile

## Description

This tile is created using the [Tile Generator](https://docs.vmware.com/en/VMware-Tanzu-Operations-Manager/3.0/tile-dev-guide/tile-generator.html) and deploys a service-broker application as a CF app. It deploys a sister project, the [ECS Service Broker](https://github.com/EMCECS/ecs-cf-service-broker/). For more instructions on using the broker once deployed, refer to the [ECS Service Broker documentation](https://emcecs.github.io/ecs-broker-tile/).

This tile implements the following tile generator errands:

* **deploy-service-broker**:  Deploy the broker as a CF app.
* **register-broker**: Register the deployed broker with CF as service broker.
* **destroy-broker**: Deregister and delete the app from CF.

Upon completion, PCF Tile will support dynamic plans which enables the broker to
be configured from the PCF Ops Manager.

## Current Status

Currently, the Tile version 2.3.3 is available for download via the [Broadcom Support portal](https://support.broadcom.com/group/ecx/productdownloads?subfamily=ECS%20Service%20Broker%20for%20VMware%20Tanzu).
* ***This is the last release of the tile, no further versions will be released.***
* ***Support for the tile will end on May 25, 2025. No support will be provided after this date.***

## Requirement

* ECS Cluster configured and running. If you do not have one please refer to [ECS Test Drive](https://portal.ecstestdrive.com) to create an account.
* ECS VIP address for Management and Object 
* Namespace and Replication group
* ECS  SSL cert, to get the ssl cert use ```openssl s_client  -connect <ecsvip>:443 –showcert ``` to get ssl

## Build Tile
* Clone the code to your local bosh machine
* Install [Tile Generator Tool](https://docs.vmware.com/en/VMware-Tanzu-Operations-Manager/3.0/tile-dev-guide/tile-generator.html)
* Run command `tile build`

## Deployment
* Using OpsManager website upload the tile
* Add tile to dashboard
* Configure tile [according to the documentation](https://emcecs.github.io/ecs-broker-tile/installing.html).
* Apply Changes
* Run cf service-brokers to check the broker status

### End-user Broker Usage

CLoud Foundry end-users can create and bind services to their applications using the `cf` CLI application.

```
cf create-service ecs-bucket unlimited my_bucket
```

This creates a bucket of the `ecs-bucket` service with the `unlimited` plan and the name: `my-bucket`.  To bind
an application to this bucket:

```
cf bind-service my-app my-bucket
```

The default will give `my-app` "full control" of the bucket.  To give a reduced set of permissions, you can provide
additional configuration parameters with the `-c` flag:

```
cf bind-service my-app my-bucket -c '{"permissions": ["read", "write"]}'
```

Valid permissions include:
 * read
 * read_acl
 * write
 * write_acl
 * execute
 * full_control
 * privileged_write
 * delete
 * none

For more information about the ECS Broker usage please refer to [ECS CF service broker](https://emcecs.github.io/ecs-broker-tile/usage.html)

### Testing

Currently, tests are implemented for tile migrations using [Jest.js](https://jestjs.io). To run the tests install the `jest-cli` globally with NPM or yarn:

```shell
# Install Jest.js
$ npm install -g jest-cli

# Run jest
$ jest
```
