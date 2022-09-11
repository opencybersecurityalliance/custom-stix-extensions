## x-oca-asset object
The `x-oca-asset` object describes an asset and its properties. 
It can be referenced to give context on events that took place on this asset.
It describes the hostname, the associated IP addresses and physical addresses of the asset.
In SIEM terminology which collects events from many systems - it is used to describe where the events took place.
It is referenced in the [`x-oca-event`](./x-oca-event.md) object.

While `x-oca-asset` specifies the host on which the associated event occurred, it may provide extenstions to describe addtional entities of tne runtime environment. In a cloud environment the event may occur within a container that is running or a partcular pod on the host. `x-oca-asset` uses a separate extension for each addtional runtime entity. Please note that as per the STIX [2.0](http://docs.oasis-open.org/cti/stix/v2.0/cs01/part3-cyber-observable-core/stix-v2.0-cs01-part3-cyber-observable-core.html#_Toc496715388)and [2.1](https://docs.oasis-open.org/cti/stix/v2.1/csprd01/stix-v2.1-csprd01.html#_Toc16070830), COOs/SCOs can have any number of extenstions.

| property name | type | description |
|--|--|--|
| type | `string` | x-oca-asset |
| name | `name` | Name of the asset |
| extensions | `dictionary` | Specifies any extensions of the object, as a dictionary. |
| device_id | `string` | The ID of the device. |
|hostname|`string`|name of this host|
|host_id|`string`|id of this host|
|ip_refs|`list` of type `object-ref`| references the ip addresses related to this host. must be `ipv4-addr` or `ipv6-addr`|
|mac_refs|`list` of type `object-ref`| references the mac addresses related to this host. must be of type `mac-addr`|
| os_ref | `object-ref` | Specifies the operating system of the asset, as a reference to the Cyber-observable Object. The object referenced must be of type `software`. |
| architecture | `string` | Architecture of the asset. |

### Container Extenstion

The container asset extension represents a container.

| property name | type | description |
|--|--|--|
| type | `string` | x-oca-container-ext |
| name | `string` | container name |
| id | `string` | container id |
| image_name | `string` | container image name |
| image_id | `string` | container image id |
| container_type | `container_type_ov` | container type | 
| privileged | `boolean` | indicates a priviliged container |

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

The pod asset extension represents an oc/k8s pod.

| property name | type | description |
|--|--|--|
| type | `string` | x-oca-pod-ext |
| name | `string` | pod name |
| ip_refs | `list` of type `object-ref` | references the ip addresses allocated to this pod. must be `ipv4-addr` or `ipv6-addr` |

### Example

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
	        "mac_refs": ["3"],
		"extensions": {
		    "x-oca-container-ext": {
                        "name": "example container",
                        "id”: “bf032feb4117",
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
	    }
    }

