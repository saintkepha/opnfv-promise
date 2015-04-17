# stormforge

A YANG module which provides a collection of Virtualized
Infrastructure Manager resource models to provide data model driven
management of resources across providers.

  [![NPM Version][npm-image]][npm-url]
  [![NPM Downloads][downloads-image]][downloads-url]

This module is maintained under direction of
[OPNFV Promise](http://wiki.opnfv.org/promise) project.

Currently planned key services are:

* Resource Capacity Management Service
* Resource Reservation Service

## Information Elements

### Resource Reservation

The data model describing the required parameters regarding a resource
reservation. The schema definition expressed in Yang can be found
[here](storms/promise/opnfv-promise-models.yang).

#### Key Elements

Name | Type | Description
---  | ---  | ---
start | ys:date-and-time | Timestamp of when the consumption of reserved resources can begin
end   | ys:date-and-time | Timestamp of when the consumption of reserved resource must end
expiry | number | Duration expressed in seconds since `start` when resource not yet allocated shall be released back to the available zone
zone | vim:AvailabilityZone | Reference to a zone where the resources will be reserved
capacity | object | Quantity of resources to be reserved per resource types
attributes | list | References to resource attributes needed for reservation
resources | list (vim:ResourceElement) | Reference to a collection of existing resource elements required

#### State Elements (read-only)

State Elements are available as part of lookup response about the data model.

Name | Type | Description
---  | ---  | ---
provider | vim:ResourceProvider | Reference to a specific provider when reservation service supports multiple providers
remaining | object | Quantity of resources remaining for consumption based on consumed allocations
allocations | list (vim:ResourceAllocation) | Reference to a collection of consumed allocations referencing this reservation

#### Notification Elements

Name | Type | Description
---  | ---  | ---
reservation-event | Event | Subscribers will be notified if the reservation encounters an error or other events

#### Inherited Elements

##### Extended from vim:ResourceElement

Name | Type | Description
---  | ---  | ---
name | string | Name of the data model
enabled | boolean | Enable/Disable the data model
protected | boolean | Prevent model from being destroyed when protected
owner | vim:AccessIdentity | An owner for the data model
visibility | enumeration | Visibility level of the given data model
tags | list (string) | List of string tags for query/filter
members | list (vim:AccessIdentity) | List of additional AccessIdentities that can operate on the data model

##### Extended from ys:DataModel

Name | Type | Description
---  | ---  | ---
id | string | A GUID identifier for the data model (usually auto-generated, but can also be specified)
createdOn | ys:date-and-time | Timestamp of when the data model was created
modifiedOn | ys:date-and-time | Timestamp of when the data model was last modified
accessedOn | ys:date-and-time | Timestamp of when the data model was last accessed

### Resource Allocation

The data model describing the required parameters regarding a resource
allocation.  The schema definition expressed in Yang can be found
[here](storms/promise/opnfv-promise-models.yang).

#### Key Elements

Name | Type | Description
---  | ---  | ---
reservation | vim:ResourceReservation | Reference to an existing reservation identifier
allocate-on-start | boolean | Specify whether the allocation can take effect automatically upon reservation 'start'
resources | list (vim:ResourceElement) | Reference to a collection of new resource elements to be allocated

#### State Elements (read-only)

Name | Type | Description
---  | ---  | ---
priority | number | Read-only state information about the priority classification of the reservation

#### Inherited Elements

##### Extended from vim:ResourceElement

Name | Type | Description
---  | ---  | ---
name | string | Name of the data model
enabled | boolean | Enable/Disable the data model
protected | boolean | Prevent model from being destroyed when protected
owner | vim:AccessIdentity | An owner for the data model
visibility | enumeration | Visibility level of the given data model
tags | list (string) | List of string tags for query/filter
members | list (vim:AccessIdentity) | List of additional AccessIdentities that can operate on the data model

##### Extended from ys:DataModel

Name | Type | Description
---  | ---  | ---
id | string | A GUID identifier for the data model (usually auto-generated, but can also be specified)
createdOn | ys:date-and-time | Timestamp of when the data model was created
modifiedOn | ys:date-and-time | Timestamp of when the data model was last modified
accessedOn | ys:date-and-time | Timestamp of when the data model was last accessed

## Installation
```bash
$ npm install stormforge
```
## Literate Coffeescript Documentation

* [YANG stormforge Module](src/stormforge.litcoffee)

## StormForge YANG Schemas
* [storm-common-models](schemas/storm-common-models.yang)
  * [storm-management-models](schemas/storm-management-models.yang)
  * [storm-resource-models](schemas/storm-resource-models.yang)
    * [storm-resource-abstract-models](schemas/storm-resource-abstract-models.yang)
	* [storm-resource-identity-models](schemas/storm-resource-identity-models.yang)
	* [storm-resource-compute-models](schemas/storm-resource-compute-models.yang)
	* [storm-resource-network-models](schemas/storm-resource-network-models.yang)
  * [storm-service-models](schemas/storm-service-models.yang)

## OPNFV Promise YANG Schemas
* [opnfv-promise](storms/promise/opnfv-promise.yang)
  * [opnfv-promise-models](storms/promise/opnfv-promise-models.yang)

## Additional YANG Schemas
* [multi-vim](storms/multi-vim/multi-vim.yang)
* [openstack](storms/openstack/openstack-resource-provider.yang)


## License
  [MIT](LICENSE)

[npm-image]: https://img.shields.io/npm/v/stormforge.svg
[npm-url]: https://npmjs.org/package/stormforge
[downloads-image]: https://img.shields.io/npm/dm/stormforge.svg
[downloads-url]: https://npmjs.org/package/stormforge
