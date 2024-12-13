## x-oca-asset SCO object
The `x-oca-asset` object is a component of telemtry that describes an asset and its properties.
It can be referenced to give context on events that took place on this asset.
It describes the hostname, the associated IP addresses and physical addresses of the asset.
In SIEM terminology which collects events from many systems - it is used to describe where the events took place.
It is referenced in the [`x-oca-event`](./x-oca-event.md) object.

While `x-oca-asset` specifies the host on which the associated event occurred, it may provide extenstions to describe addtional entities of tne runtime environnment. In a cloud environment the event may occur within a container that is running or a partcular pod on the host. `x-oca-asset` uses a separate extension for each addtional runtime entity. Please note that as per the STIX [2.0](http://docs.oasis-open.org/cti/stix/v2.0/cs01/part3-cyber-observable-core/stix-v2.0-cs01-part3-cyber-observable-core.html#_Toc496715388)and [2.1](https://docs.oasis-open.org/cti/stix/v2.1/csprd01/stix-v2.1-csprd01.html#_Toc16070830), COOs/SCOs can have any number of extenstions.

| property name | type | description |
|--|--|--|
| **type** (required) | `string` | x-oca-asset |
| **id** (required) | `string` | A valid [stix-id](https://docs.oasis-open.org/cti/stix/v2.1/os/stix-v2.1-os.html#_64yvzeku5a5c) |
| **spec_version** (optional) | `string` | The value of this property MUST be 2.1 for STIX Objects defined according to this specification. |
| **extensions** | `dictionary` | Specifies any extensions of the object, as a dictionary. |
| **device_id** | `string` | The ID of the device. |
| **hostname** (required)|`string`|The name of this host|
| **ip_refs**|`list` of type `object-ref`| references the ip addresses related to this host. must be `ipv4-addr` or `ipv6-addr`|
| **mac_refs**|`list` of type `object-ref`| references the mac addresses related to this host. must be of type `mac-addr`|
| **os_ref**| `object-ref` | Specifies the operating system of the asset, as a reference to the Cyber-observable Object. The object referenced must be of type `software`. |
| **architecture** | `string` | Architecture of the asset. |
| **uptime** | `string` | Specifies the seconds the asset has been up.|
| **host_type** | `string` | Specifies the type of asset. Example, firewall, t2.micro etc.|
| **ingress** | `x-oca-traffic-type` | Specifies information like interface number and name, vlan, and zone information to classify ingress traffic using the Traff9c-type sub-object.|
| **egress** | `x-oca-traffic-type` | Specifies information like interface number and name, vlan, and zone information to classify egress traffic using the Traffic-type sub object.|
| **geo_ref**|`object-ref`| references the geolocation of this host. must be of type `x-oca-geo`|

### Container Extenstion

Extension Name `x-oca-container-ext`

The container asset extension represents a container.

| property name | type | description |
|--|--|--|
| **type** | `string` | x-oca-container-ext |
| **name** | `string` | container name |
| **container_id** | `string` | container id |
| **image_name** | `string` | container image name |
| **image_id** | `string` | container image id |
| **container_type** | `container_type_ov` | container type |
| **privileged** | `boolean` | indicates a priviliged container |

#### Container Type Vocabluary

Vocabulary Name: `container-type-ov`

An open vocabulary for the container_type field of the container extension of an asset object.

| Vocabulary Value | Description |
|--|--|
| `docker` | Specifies a docker container |
| `crio` | Specifies a crio container |
| `mesos` | Specifies a mesos container |
| `lxc` | Specifies a LXC container |
| `libvirt_lxc` | Specifies a libvirt LXC container |
| `rkt` | Specifies a rkt container |
| `oci` | Specifies a oci standards based container |
| `custom` |Specifies a custom container |

### Pod Extenstion

Extension Name `x-oca-pod-ext`

The pod asset extension represents an oc/k8s pod.

| property name | type | description |
|--|--|--|
| **type** | `string` | x-oca-pod-ext |
| **name** | `string` | pod name |
| **ip_refs** | `list` of type `object-ref` | references the ip addresses allocated to this pod. must be `ipv4-addr` or `ipv6-addr` |

#### Traffic Type Sub-Object

Type Name `x-oca-traffic-type`

| value | type | description |
|--|--|--|
| **zone** | `string` | Specifies the network zone of the inbound or outbound traffic.|
| **interfaces** | list of type `x-oca-interface-type` | Specifies the interface information. Each dictionary key SHOULD come from the Interface vocabulary. |

#### Interface Type Sub-Object

Type Name `x-oca-interface-type`

| value | type | description |
|--|--|--|
| **alias** | `string` | Specifies the interface alias as reported by the system. |
| **interface_id** | `string` | Specifies the interface ID. |
| **name** | `string` | Specifies the interface name as reported by the system.|

### Example 1

```json
    {
	    "0":
	    {
	        "type": "ipv4-addr",
	        "value": "9.9.9.9"
	    },
	    "1":
	    {
	        "type": "x-oca-asset",
	        "ip_refs": ["0", "2"],
	        "hostname": "example host",
	        "host_id": "123A",
          "geo_ref": "5",
          "mac_refs": ["3"],
          "host_type": "APM Server",
          "egress":
          {
            "zone": "internal",
            "interfaces": [
              {
                "alias": "inside",
                "interface_id": "10",
                "name", "eth0"
              }
            ]
          },
          "extensions": {
            "x-oca-container-ext": {
                  "name": "example container",
                  "container_id": "bf032feb4117",
                  "image_id": "92b1b5d66457...",
                  "image_name": "us.icr.io/...",
                  "container_type": "crio"
            },
            "x-oca-pod-ext": {
                  "name": "example pod",
                  "ip_refs": ["4"]
            }
          }
	    },
	    "2":
	    {
	        "type": "ipv6-addr",
	        "value": "ffff:1111:ffff:1111:ffff:1111:ffff:1111",
	        "resolves_to_refs": ["7"]
	    },
	    "3":
	    {
	        "type": "mac-addr",
	        "value": "00-00-11-00-22-00"
	    },
	    "4":
	    {
	        "type": "ipv4-addr",
	        "value": "192.168.xxx.yyy"
	    },
      "5": {
          "type": "x-oca-geo",
          "name": "Dallas-1",
          "time_zone": "America/Chicago",
          "country_iso_code": "US",
          "country_name": "United States of America",
          "location": {
            "lon": "-96.800496798",
            "lat": "32.785663524"
          }
      }
  }
  ```



### Example 2: Stix 2.1
The Observed Data SDO can only gather any SCO's (Observables), while the Sighting SRO is used to combine these observations with appropriate SDO's, such as `x-oca-asset` or `x-oca-geo`.

```json
[
  {
    "type": "ipv4-addr",
    "spec_version": "2.1",
    "id": "ipv4-addr--38609426-bc06-5cbc-9763-e77e99c9d9e4",
    "value": "9.9.9.9"
  },
  {
    "type": "x-oca-asset",
    "spec_version": "2.1",
    "id": "x-oca-asset--fec3de6d-bfc4-4ef3-9f4b-c21aa2d57e7a",
    "created": "2024-09-01T06:55:35.241Z",
    "modified": "2024-09-01T06:55:35.241Z",
    "ip_refs": [
      "ipv4-addr--38609426-bc06-5cbc-9763-e77e99c9d9e4",
      "ipv6-addr--dc0ef52f-b6cf-52a0-a6a1-977b32a57063"
    ],
    "hostname": "example host",
    "host_id": "123A",
    "geo_ref": "x-oca-geo--419f0ac4-2836-46f0-9985-820f7a4b7abc",
    "mac_refs": [
      "mac-addr--b5dbdbbb-5470-58c8-9b86-81b7d83a770b"
    ],
    "host_type": "APM Server",
    "egress": {
      "zone": "internal",
      "interfaces": [
        {
          "alias": "inside",
          "interface_id": "10",
          "name": "eth0"
        }
      ]
    },
    "extensions": {
      "x-oca-container-ext": {
        "name": "example container",
        "container_id": "bf032feb4117",
        "image_id": "92b1b5d66457...",
        "image_name": "us.icr.io/...",
        "container_type": "crio"
      },
      "x-oca-pod-ext": {
        "name": "example pod",
        "ip_refs": [
          "ipv4-addr--f1958dd5-5175-5702-beef-742d2cf3c0ec"
        ]
      }
    }
  },
  {
    "type": "ipv6-addr",
    "spec_version": "2.1",
    "id": "ipv6-addr--dc0ef52f-b6cf-52a0-a6a1-977b32a57063",
    "value": "ffff:1111:ffff:1111:ffff:1111:ffff:1111",
    "resolves_to_refs": [
      "mac-addr--b5dbdbbb-5470-58c8-9b86-81b7d83a770b"
    ]
  },
  {
    "type": "mac-addr",
    "spec_version": "2.1",
    "id": "mac-addr--b5dbdbbb-5470-58c8-9b86-81b7d83a770b",
    "value": "00-00-11-00-22-00"
  },
  {
    "type": "ipv4-addr",
    "spec_version": "2.1",
    "id": "ipv4-addr--f1958dd5-5175-5702-beef-742d2cf3c0ec",
    "value": "192.168.xxx.yyy"
  },
  {
    "type": "x-oca-geo",
    "spec_version": "2.1",
    "id": "x-oca-geo--419f0ac4-2836-46f0-9985-820f7a4b7abc",
    "created": "2024-09-01T06:55:32.781Z",
    "modified": "2024-09-01T06:55:32.781Z",
    "name": "Dallas-1",
    "time_zone": "America/Chicago",
    "country_iso_code": "US",
    "country_name": "United States of America",
    "location": {
      "lon": "-96.800496798",
      "lat": "32.785663524"
    }
  },
  {
    "type": "observed-data",
    "spec_version": "2.1",
    "id": "observed-data--b67d30ff-02ac-498a-92f9-32f845f448cf",
    "created_by_ref": "identity--e5f1b90a-d9b6-40ab-81a9-8a29df4b6b65",
    "created": "2016-04-06T19:58:16.000Z",
    "modified": "2016-04-06T19:58:16.000Z",
    "first_observed": "2015-12-21T19:00:00Z",
    "last_observed": "2015-12-21T19:00:00Z",
    "number_observed": 50,
    "object_refs": [
      "ipv4-addr--38609426-bc06-5cbc-9763-e77e99c9d9e4",
      "ipv6-addr--dc0ef52f-b6cf-52a0-a6a1-977b32a57063",
      "mac-addr--b5dbdbbb-5470-58c8-9b86-81b7d83a770b",
      "ipv4-addr--f1958dd5-5175-5702-beef-742d2cf3c0ec"
    ]
  },
  {
    "type": "sighting",
    "spec_version": "2.1",
    "id": "sighting--49cc5c32-98b8-4d15-94bf-2f867d71a2fa",
    "created": "2023-11-18T05:26:43.45768Z",
    "modified": "2023-11-18T05:26:43.45768Z",
    "sighting_of_ref": "x-oca-asset--fec3de6d-bfc4-4ef3-9f4b-c21aa2d57e7a",
    "where_sighted_refs": [
          "x-oca-geo--419f0ac4-2836-46f0-9985-820f7a4b7abc"
    ],
    "observed_data_refs": [
      "observed-data--b67d30ff-02ac-498a-92f9-32f845f448cf"
    ]
  }
]
  ```