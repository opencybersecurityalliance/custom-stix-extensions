## x-ibm-finding object

The `x-ibm-finding` SCO object describes a threat, policy, violation, or alert and its associated properties. 
Where possible, references are made to existing STIX objects (ie. ip addresses, users).


| **Property Name** | **Type** | **Description** |
|---------------|------|-------------|
| **type** (required) | `string` | The value of this property must be `x-ibm-finding`. |
| **id** (required) | `string` | A valid [stix-id](https://docs.oasis-open.org/cti/stix/v2.1/os/stix-v2.1-os.html#_64yvzeku5a5c) based on`x-ibm-ttp-tagging` |
| **spec_version** (optional) | `string` | The value of this property MUST be 2.1 for STIX Objects defined according to this specification. |
| **finding_type** (required) | `string` | An open vocabulary that identifies the finding type. (ie. `threat`, `policy`, `violation`, `alert`.) |
| **name** (required) | `string` | The name of the threat, policy, violation, or  alert. |
| **alert_id** | `string` | The id of the finding from the data source |
| **description** | `string` | The description of the finding. |
| **src_ip_ref** | `object-ref` | Specifies the source ip address of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `ipv4-addr` or `ipv6-addr`. |
| **dst_ip_ref** | `object-ref` | Specifies the destination ip address of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `ipv4-addr` or `ipv6-addr`. |
| **src_os_ref** | `object-ref` | Specifies the source operating system of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `software`. |
| **dst_os_ref** | `object-ref` | Specifies the destination operating system of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `software`. |
| **src_application_ref** | `object-ref` | Specifies the source application of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `software`. |
| **dst_application_ref** | `object-ref` | Specifies the destination application of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `software`. |
|**src_geo_ref** | `object-ref` | Specifies the source geographic location of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `x-oca-geo`.|
|**dst_geo_ref** | `object-ref` | Specifies the destination geographic location of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `x-oca-geo`.|
| **src_device** | `string` | Specifies the source device of the finding. (ie. database, browser) |
| **dst_device** | `string` | Specifies the destination device of the finding. (ie. database, browser) |
| **src_application_user_ref** | `object-ref` | Specifies the source application user of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `user-account`. |
| **dst_application_user_ref** | `object-ref` | Specifies the destination application user of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `user-account`. |
| **src_database_user_ref** | `object-ref` | Specifies the source database user of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `user-account`. |
| **dst_database_user_ref** | `object-ref` | Specifies the destination database user of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `user-account`. |
| **src_os_user_ref** | `object-ref` | Specifies the source operating system user of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `user-account`. |
| **dst_os_user_ref** | `object-ref` | Specifies the destination operating system user of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `user-account`. |
| **severity** | `number` | Severity of the finding on a scale of 1-100. |
| **confidence** | `number` | Confidence of the finding on a scale of 1-100. |
| **magnitude** | `number` | Magnitude of the finding on a scale of 1-100. |
| **rule_trigger_count** | `number` | The number of rules that were triggered in the finding. |
| **rule_names** | `list` of type `string` | The rules that were triggered by the finding. |
| **event_count** | `number` | The number of events found in the finding. |
| **time_observed** | `timestamp` | The time in UTC when the finding was observed. |
| **start** | `timestamp` | The start time in UTC of the finding. |
| **end** | `timestamp` | The end time in UTC of the finding. |
| **ttp_tagging_refs** | `list` of type `identifier` | List of objects reffering to [x-ibm-ttp-tagging](x-ibm-ttp-tagging.md) describing techniques tactics and procedures mapped to this finding, such as MITRE ATT&CK TTP's |
| **ioc_refs** | `list` of type `object-ref` | References indicators of compromise related to this finding. Must be of type `file`, `ipv4-addr`, `ipv6-addr`, `domain`, `url` |

### Example:

```javascript
{
      "type": "observed-data",
      "id": "observed-data--ed82dd61-cc41-485b-b608-d278469e6259",
      "created_by_ref": "identity--33fa3e56-6511-40de-bc69-c5ffeb3838f9",
      "created": "2019-07-18T19:11:07.537Z",
      "modified": "2019-07-18T19:11:07.537Z",
      "first_observed": "2019-07-18T19:06:20.459257Z",
      "last_observed": "2019-07-18T19:08:10.111663Z",
      "number_observed": 1,
      "objects": {
        "0": {
          "type": "ipv4-addr",
          "value": "127.0.0.1"
        },
        "1": {
          "type": "ipv4-addr",
          "value": "192.168.0.12"
        },
        "2": {
          "type": "user-account",
          "user_id": "danny.elliott@ibm.com"
        },
        "3": {
          "type": "software",
          "name": "Windows",
          "version": "10.0"
        },
        "4": {
          "type": "x-ibm-finding",
          "name": "Some rule name",
          "finding_type": "violation",
          "time_observed": "2019-07-18T19:06:20.459257Z",
          "severity": 80,
          "src_ip_ref": "0",
          "dst_ip_ref": "1",
          "src_application_user_ref": "2",
          "src_application_ref": "3",
          "src_geo_ref": "8",
          "src_device": "Chrome",
          "ttp_tagging_refs": [5], 
          "ioc_refs": ["6","7"]
       },
       "5": {
          "type": "x-ibm-ttp-tagging",
          "name": "Active Scanning",
          "url": "https://attack.mitre.org/versions/v8/techniques/T1595/",
          "confidence": 0.8,
          "kill_chain_phases": [
             {
                "kill_chain_name": "mitre-attack",
                "phase_name": "reconnaissance"
             }
          ],
          "extensions": 
          {
             "mitre-attack-ext": 
             {
                "tactic_id": "TA0043",
                "tactic_url": "https://attack.mitre.org/versions/v8/tactics/TA0043/",
                "tactic_name": "Reconnaissance",
                "technique_id": "T1595",
                "technique_url": "https://attack.mitre.org/versions/v8/techniques/T1595/",
                "technique_name": "Active Scanning"
             }
          }
        },
        "6": {
                "type": "ipv4-addr",
                "value": "13.14.1.1"
             },
        "7": {
                "type": "url",
                "value": "http://maliciousmalware.bad"
        },
        "8": {
                "type": "x-oca-geo",
                "country_iso_code": "US"
        }
    }
}
```

## Example 2: Stix v2.1 List
The Observed Data SDO uses the `object_refs` property to contian id's of any observables, and each observable previously contained in the `object` property now needs to be provided with an `id` property as a minimum

```json
[
  {
    "type": "observed-data",
    "id": "observed-data--ed82dd61-cc41-485b-b608-d278469e6259",
    "created_by_ref": "identity--33fa3e56-6511-40de-bc69-c5ffeb3838f9",
    "created": "2019-07-18T19:11:07.537Z",
    "modified": "2019-07-18T19:11:07.537Z",
    "first_observed": "2019-07-18T19:06:20.459257Z",
    "last_observed": "2019-07-18T19:08:10.111663Z",
    "number_observed": 1,
    "object_refs": [
      "ipv4-addr--efcd5e80-570d-4131-b213-62cb18eaa6a8",
      "ipv4-addr--5853f6a4-638f-5b4e-9b0f-ded361ae3812",
      "user-account--0d5b424b-93b8-5cd8-ac36-306e1789d63c",
      "software--a1827f6d-ca53-5605-9e93-4316cd22a00a",
      "ipv4-addr--157aeca1-b949-5c83-89cb-ef99757be9c6",
      "x-ibm-finding--2ca1326a-122e-4fdf-ac4c-a72942af260c",
      "url--e9653306-7457-5316-a478-57559c06d87f",
      "x-oca-geo--ed82dd61-cc41-485b-b608-d278469e6259"
    ]
  },
  {
    "type": "ipv4-addr",
    "spec_version": "2.1",
    "id": "ipv4-addr--efcd5e80-570d-4131-b213-62cb18eaa6a8",
    "value": "127.0.0.1"
  },
  {
    "type": "ipv4-addr",
    "spec_version": "2.1",
    "id": "ipv4-addr--5853f6a4-638f-5b4e-9b0f-ded361ae3812",
    "value": "192.168.0.12"
  },
  {
    "type": "user-account",
    "spec_version": "2.1",
    "id": "user-account--0d5b424b-93b8-5cd8-ac36-306e1789d63c",
    "user_id": "danny.elliott@ibm.com"
  },
  {
    "type": "software",
    "spec_version": "2.1",
    "id": "software--a1827f6d-ca53-5605-9e93-4316cd22a00a",
    "name": "Windows",
    "version": "10.0"
  },
  {
    "type": "x-ibm-finding",
    "spec_version": "2.1",
    "id": "x-ibm-finding--2ca1326a-122e-4fdf-ac4c-a72942af260c",
    "name": "Some rule name",
    "finding_type": "violation",
    "time_observed": "2019-07-18T19:06:20.459257Z",
    "severity": 80,
    "src_ip_ref": "0",
    "dst_ip_ref": "1",
    "src_application_user_ref": "2",
    "src_application_ref": "3",
    "src_geo_ref": "8",
    "src_device": "Chrome",
    "ttp_tagging_refs": [
      "x-ibm-ttp-tagging--fa5c2b89-ede5-425e-8d65-95dedb2d444f"
    ],
    "ioc_refs": [
      "ipv4-addr--157aeca1-b949-5c83-89cb-ef99757be9c6",
      "url--e9653306-7457-5316-a478-57559c06d87f"
    ]
  },
  {
    "type": "x-ibm-ttp-tagging",
    "spec_version": "2.1",
    "id": "x-ibm-ttp-tagging--fa5c2b89-ede5-425e-8d65-95dedb2d444f",
    "name": "Active Scanning",
    "url": "https://attack.mitre.org/versions/v8/techniques/T1595/",
    "confidence": 0.8,
    "kill_chain_phases": [
      {
        "kill_chain_name": "mitre-attack",
        "phase_name": "reconnaissance"
      }
    ],
    "extensions": {
      "mitre-attack-ext": {
        "tactic_id": "TA0043",
        "tactic_url": "https://attack.mitre.org/versions/v8/tactics/TA0043/",
        "tactic_name": "Reconnaissance",
        "technique_id": "T1595",
        "technique_url": "https://attack.mitre.org/versions/v8/techniques/T1595/",
        "technique_name": "Active Scanning"
      }
    }
  },
  {
    "type": "ipv4-addr",
    "spec_version": "2.1",
    "id": "ipv4-addr--157aeca1-b949-5c83-89cb-ef99757be9c6",
    "value": "13.14.1.1"
  },
  {
    "type": "url",
    "spec_version": "2.1",
    "id": "url--e9653306-7457-5316-a478-57559c06d87f",
    "value": "http://maliciousmalware.bad"
  },
  {
    "type": "x-oca-geo",
    "spec_version": "2.1",
    "id": "x-oca-geo--ed82dd61-cc41-485b-b608-d278469e6259",
    "created": "2019-07-18T19:11:07.537Z",
    "modified": "2019-07-18T19:11:07.537Z",
    "country_iso_code": "US"
  }
]
```