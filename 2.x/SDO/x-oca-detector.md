## x-oca-detector

x-oca-detector objects define tools, software, products, etc. that are capable of performing
detection. They may also represent a more abstract method of detection such as a Sigma rule. They
should be related to one or more Detection obects.

| property name            | type                       | description
|--------------------------|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **type** (required)          | `string`                   | MUST be the literal "x-oca-detector" |
| **id** (required) | `string` | A valid [stix-id](https://docs.oasis-open.org/cti/stix/v2.1/os/stix-v2.1-os.html#_64yvzeku5a5c) |
| **spec_version** (required) | `string` | The value of this property MUST be 2.1 for STIX Objects defined according to this specification. |
| **created** (required) | `timestamp` | The date and time the object was created |
| **modified** (required) | `timestamp` | The date and time the object was modified |
| **name** (required)          | `string`                   | The name used to identify the Detector. |
| **description**              | `string`                   | Description of the Detector. |
| **cpe**                      | `string`                   | A valid CPE string. |
| **valid_until**              | `timestamp`                | The time at which this Detector should no longer be considered valuable intelligence. |
| **vendor**                   | `string`                   | The vendor name of the Detector. |
| **vendor_url**               | `string`                   | A url that links to the vendor of the Detector's primary website. |
| **product**                  | `string`                   | The product name of the Detector. |
| **product_url**              | `string`                   | A url that links to an official download of the Detector product or a primary website describing the Detector product. |
| **detection_types**          | `list` of type `string`    | A list of the types of detections the detector can perform. For example: beacon, phishing, exfiltration. |
| **detector_data_categories** | `list` of type `string`    | A list of the general catagories of data the detector uses. For example: network, endpoint, etc. |
| **detector_data_sources**    | `list` of type `string`    | A list of the specific data sources the detector uses. For example: pcap, windows security event logs, sysmon, etc. |

## Extension Definition

```json
{
  "type": "extension-definition",
  "spec_version": "2.1",
  "id": "extension-definition--5cccba5c-0be4-450c-8672-b66e98515754",
  "created_by_ref": "identity--b085a68a-bf48-4316-9667-37af78cba894",
  "created": "2023-05-01T12:00:00.000Z",
  "modified": "2023-05-01T12:00:00.000Z",
  "name": "x-oca-detector Extension Definition",
  "description": "This schema creates a new object type called detector, which describes software that is capable of performing detections.",
  "schema": "https://raw.githubusercontent.com/opencybersecurityalliance/stix-extensions/main/2.x/schemas/x-oca-detector.json",
  "version": "1.0.0",
  "extension_types": [
    "new-sdo"
  ]
}
```

## Examples

### Zeek Detector

```json
{
  "type": "x-oca-detector",
  "spec_version": "2.1",
  "id": "x-oca-detector--67330653-ac02-46c8-b9c2-25b837a2ed6d",
  "created_by_ref": "identity--b085a68a-bf48-4316-9667-37af78cba894",
  "created": "2023-05-01T12:00:00.000Z",
  "modified": "2023-05-01T12:00:00.000Z",
  "name": "Zeek",
  "description": "A network security monitoring tool.",
  "cpe": "cpe:2.3:a:zeek:zeek:5.0.9:*:*:*:*:*:*:*",
  "vendor": "Zeek",
  "vendor_url": "https://zeek.org",
  "product": "Zeek",
  "product_url": "https://zeek.org/get-zeek/",
  "product_version": "5.0.9",
  "detection_types": ["dcsync"],
  "detector_data_categories": ["network"],
  "detector_data_sources": ["network tap"],
  "valid_until": "2027-05-01T12:00:00.000Z",
  "extensions": {
    "extension-definition--5cccba5c-0be4-450c-8672-b66e98515754": {
      "extension_type": "new-sdo"
    }
  }
}
```

### Sigma Rule Detector

```json
{
  "type": "x-oca-detector",
  "spec_version": "2.1",
  "id": "x-oca-detector--f9ccdd3d-2217-45fd-8e65-055da8e66c3e",
  "created_by_ref": "identity--b085a68a-bf48-4316-9667-37af78cba894",
  "created": "2023-05-01T12:00:00.000Z",
  "modified": "2023-05-01T12:00:00.000Z",
  "name": "Sigma",
  "description": "A generic signature format for log files.",
  "cpe": "cpe:2.3:a:sigmahq:sigma:0.21:*:*:*:*:*:*:*",
  "vendor": "SigmaHQ",
  "vendor_url": "https://github.com/SigmaHQ",
  "product": "Sigma",
  "product_url": "https://github.com/SigmaHQ/sigma",
  "product_version": "0.21",
  "detection_types": ["log"],
  "detector_data_categories": ["log"],
  "detector_data_sources": ["windows event log", "sysmon", "zeek", "rita"],
  "valid_until": "2027-05-01T12:00:00.000Z",
  "extensions": {
    "extension-definition--5cccba5c-0be4-450c-8672-b66e98515754": {
      "extension_type": "new-sdo"
    }
  }
}
```
