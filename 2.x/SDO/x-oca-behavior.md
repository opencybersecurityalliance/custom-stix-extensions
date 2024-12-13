## x-oca-behavior

Adds a new object for describing adversary behaviors.
STIX supports Attack Pattern and STIX cyber observable objects (SCOs); however, we wish to describe
an object more specific than an Attack Pattern, but more general than an SCO.
For example, an Attack Pattern for spearphishing may refer to MITRE ATT&CK T1566.002 Spearphishing
Link. A Behavior may be the mail client opening a web browser. The SCOs may be the processes
involved.
The `x-oca-behavior` SDO implements this functionality.

| property name            | type                       | description
|--------------------------|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **type** (required)          | `string`                   | MUST be the literal "x-oca-behavior" |
| **id** (required) | `string` | A valid [stix-id](https://docs.oasis-open.org/cti/stix/v2.1/os/stix-v2.1-os.html#_64yvzeku5a5c) |
| **spec_version** (required) | `string` | The value of this property MUST be 2.1 for STIX Objects defined according to this specification. |
| **created** (required) | `timestamp` | The date and time the object was created |
| **modified** (required) | `timestamp` | The date and time the object was modified |
| **name** (required)          | `string`                   | The name used to identify the Behavior. |
| **description**              | `string`                   | Description of the Behavior. |
| **behavior_class**           | `string`                   | The class of behavior. The value for this property SHOULD come from the behavior-class-ov open vocabulary. |
| **tactic**                   | `string`                   | MITRE ATT&CK tactic of the Behavior. |
| **technique**                | `string`                   | MITRE ATT&CK technique of the Behavior. |
| **first_seen**               | `timestamp`                | The first_seen property represents the time that this behavior was first seen. The timestamp value MUST be precise to the nearest millisecond. |
| **platforms**                | `dictionary`               | Platforms the Behavior was seen on. Each entry may list contextual data about the platform such as the OS and OS version number. |

### Behavior Class Vocabulary

Vocabulary Name: `behavior-class-ov`

An open vocabulary for the behavior_class field of a behavior object.

| value     | description
|--|--|
| anomalous | Unusual behavior
| normal    | Usual behavior
| emergent  | New behavior not considered abnormal
| missing   | Normal behavior not present

## Extension Definition

```json
{
  "type": "extension-definition",
  "spec_version": "2.1",
  "id": "extension-definition--9c59fd79-4215-4ba2-920d-3e4f320e1e62",
  "created_by_ref": "identity--b085a68a-bf48-4316-9667-37af78cba894",
  "created": "2022-03-31T13:00:00.000Z",
  "modified": "2022-03-31T13:00:00.000Z",
  "name": "x-oca-behavior Extension Definition",
  "description": "This schema creates a new object type called x-oca-behavior. x-oca-behavior objects describe higher-level functionality than can be described using SCOs.",
  "schema": "https://raw.githubusercontent.com/opencybersecurityalliance/stix-extensions/main/2.x/schemas/x-oca-behavior.json",
  "version": "1.0.0",
  "extension_types": [
    "new-sdo"
  ]
}
```

## Examples

### Mail Client Opens Browser Behavior

```json
{
  "type": "x-oca-behavior",
  "spec_version": "2.1",
  "id": "x-oca-behavior--edc99806-f8e9-4ee3-b2d4-1234567890ab",
  "created_by_ref": "identity--b085a68a-bf48-4316-9667-37af78cba894",
  "created": "2022-03-31T13:00:00.000Z",
  "modified": "2022-03-31T13:00:00.000Z",
  "name": "Spearphish: Mail Client Opens Browser",
  "description": "An email client has opened a web browser. Although most instances of this behavior are benign, it may indicate a victim clicking on a phishing link.",
  "behavior_class": "anomalous",
  "tactic": "INITIAL ACCESS",
  "technique": "T1566.002 Spearphishing Link",
  "first_seen": "2022-03-31T13:00:00.000Z",
  "platforms": [
    {
      "operating_system": "Microsoft Windows",
      "version": "10"
    }
  ],
  "extensions": {
    "extension-definition--9c59fd79-4215-4ba2-920d-3e4f320e1e62": {
      "extension_type": "new-sdo"
    }
  }
}
```

### Registry Key Modified Behavior

```json
{
  "type": "x-oca-behavior",
  "spec_version": "2.1",
  "id": "x-oca-behavior--edc99806-f8e9-4ee3-b2d4-1234567890cc",
  "created_by_ref": "identity--b085a68a-bf48-4316-9667-37af78cba894",
  "created": "2022-03-31T13:00:00.000Z",
  "modified": "2022-03-31T13:00:00.000Z",
  "name": "Registry modification for Persistence",
  "description": "Modification of the Windows Registry may indicate an adversary attempting to establish persistence.",
  "behavior_class": "anomalous",
  "tactic": "Persistence",
  "technique": "T1547.001 - Autostart Execution - Registry Run Keys / Startup Folder",
  "first_seen": "2022-03-31T13:00:00.000Z",
  "platforms": [
    {
      "operating_system": "Microsoft Windows",
      "version": "10"
    }
  ],
  "extensions": {
    "extension-definition--9c59fd79-4215-4ba2-920d-3e4f320e1e62": {
      "extension_type": "new-sdo"
    }
  }
}
```
