## x-oca-geo object
The `x-oca-geo` object describes a specific location related to an event and its properties. 
It can be referenced to describe the geolocation information derived from techniques such as Geo IP, IP Location etc or user-supplied.

Please note that this object mimics the attributes of the [Location SDO](https://docs.oasis-open.org/cti/stix/v2.1/os/stix-v2.1-os.html#_th8nitr8jb4k)

| **property name** | **type** | **description** |
|--|--|--|
| **type** | `string` | x-oca-geo |
| **id** (required) | `string` | A valid [stix-id](https://docs.oasis-open.org/cti/stix/v2.1/os/stix-v2.1-os.html#_64yvzeku5a5c) based on`x-ibm-ttp-tagging` |
| **spec_version** (optional) | `string` | The value of this property MUST be 2.1 for STIX Objects defined according to this specification. |
| **extensions** | `dictionary` | Specifies any extensions of the object, as a dictionary. |
| **city_name** | `string` | The city that this geolocation describes. |
| **continent_name** |`string`| Specifies the name of the continent.  |
| **country_iso_code** |`string`| Specifies the ISO code of the country.  |
| **country_name** |`string`| Specifies the name of the country.|
| **location** |`x-oca-location-type`| Specifies the longitude and latitude of the location. Each dictionary key SHOULD come from the location coordinates vocabulary. |
| **name** |`string`| Specifies a user-defined description of the location. This is not typically used in automated geolocation. |
| **region_iso_code** |`string`| Specifies the region ISO code. |
| **region_name** |`string`| Specifies the region name. |
| **time_zone** |`string`| Specifies the time zone of the geolocation such as an IANA time zone name |

### Location coordinates Type Sub Object

Type Name `x-oca-location-type`

| value | type | description |
|--|--|--|
| **lon** | `double` | Specifies the longitude of the location. |
| **lat** | `double` | Specifies the latitude of the location. |

### Example

    {
	    "0":
	    {
	        "type": "x-oca-geo",
	        "name": "Dallas-1",
			"time_zone": "America/Chicago",
			"country_iso_code": "US",
			"country_name": "United States of America",
			"location":
				"lon": "-96.800496798",
				"lat": "32.785663524"
	    }
    }



### Example 2
Stix v2.1 requires observables to include an `id` property, using a UUID5 based ona key value.

```json
[
    {
        "type": "x-oca-geo",
        "id": "x-oca-geo--ed82dd61-cc41-485b-b608-d278469e6259",
        "name": "Dallas-1",
        "time_zone": "America/Chicago",
        "country_iso_code": "US",
        "country_name": "United States of America",
        "location": {
            "lon": "-96.800496798",
            "lat": "32.785663524"
        }
    }
]
```
