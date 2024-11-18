## x-ibm-ttp-tagging object
The `x-ibm-ttp-tagging` SDO describes mappings of an `x-ibm-finding` or any other object or event to a TTP (techniues tactics and procedures). It may accomodate TTP's from multiple definitions and may include extensions for defining framework specific data, such as the MITRE Att&ck extension.


| Property Name | Type | Description |
|---------------|------|-------------|
| **type** (required) | `string` | The value of this property must be `x-ibm-ttp-tagging`. |
| **id** (required) | `string` | A valid [stix-id](https://docs.oasis-open.org/cti/stix/v2.1/os/stix-v2.1-os.html#_64yvzeku5a5c) based on`x-ibm-ttp-tagging` |
| **spec_version** (optional) | `string` | The value of this property MUST be 2.1 for STIX Objects defined according to this specification. |
| **name** (required) | `string` | A name describing the tagged TTP |
| **url** (optional) | `string` | A URL reference to an external resource |
| **confidence** (optional) | `float` | A confidence level in the relevance of this tagging between 0 to 1, 1 being the highest. |
| **kill-chain-phases** (optional) | `list` of type `kill-chain-phase` | The kill chain phases this mapping is related to |

### Example 1:

```javascript
{
    "type": "x-ibm-ttp-tagging",
    "name": "Active Scanning",
    "url": "https://attack.mitre.org/versions/v8/techniques/T1595/",
    "confidence": 0.8,
    "kill_chain_phases": [
       {
          "kill_chain_name": "mitre-attack",
          "phase_name": "reconnaissance"
       }
    ]
}
```


## mitre-attack-ext Extension

Extension Name `mitre-attack-ext`

This extension includes specific taggings to the MITRE ATT&CK framework.
The key for this extension when used in the extensions dictionary **MUST** be `mitre-attack-ext`.

| Property Name | Type | Description |
|---------------|------|-------------|
| **tactic_id** (optional) | `string` | The external ID of the tactic as TAXXXX where the X states the tactic id |
| **tactic_url** (optional) | `string` | The URL pointing to the documentation of the tactic in the MITRE ATT&CK website |
| **tactic_name** (required) | `string` | The name of the tactic |
| **technique_id** (optional) | `string` | The external ID of the technique as TXXXX.YYY where the X states the technique id and if it is a sub technique X is followed by .YYY where Y is the sub technique id |
| **technique_url** (optional) | `string` | The URL pointing to the documentation of the technique in the MITRE ATT&CK website |
| **technique_name** (optional) | `string` | The name of the technique |

### Example 1:

```json
{
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
}

```

