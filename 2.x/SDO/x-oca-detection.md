## x-oca-detection

Adds a new object for detecting adversary behaviors. STIX Indicators support the creation of
patterns to detect indicators of compromise. We wish to extend this to adversary behaviors using
Detection objects. For example, a Detection object for detecting the behavior of a mail client
opening a web browser may contain an analytic that matches the parent and child process names with
common mail clients and web browsers, respectively.

| property name            | type                       | description
|--------------------------|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **type** (required)          | `string`                   | MUST be the literal "x-oca-detection" |
| **id** (required) | `string` | A valid [stix-id](https://docs.oasis-open.org/cti/stix/v2.1/os/stix-v2.1-os.html#_64yvzeku5a5c) |
| **spec_version** (required) | `string` | The value of this property MUST be 2.1 for STIX Objects defined according to this specification. |
| **created** (required) | `timestamp` | The date and time the object was created |
| **modified** (required) | `timestamp` | The date and time the object was modified |
| **name** (required)          | `string`                   | The name used to identify the Detection. |
| **data_sources** (required)  | `list` of type `dictionary`| Information about the data event that the detection targets. |
| **analytic** (required)      | `dictionary`               | Base64 encoded logic defining the detection along with the type of rule (e.g. Sigma rule).|

## Extension Definition

```json
{
  "type": "extension-definition",
  "spec_version": "2.1",
  "id": "extension-definition--c4690e13-107e-4796-8158-0dcf1ae7bc89",
  "created_by_ref": "identity--b085a68a-bf48-4316-9667-37af78cba894",
  "created": "2022-03-31T13:00:00.000Z",
  "modified": "2022-03-31T13:00:00.000Z",
  "name": "x-oca-detection Extension Definition",
  "description": "This schema creates a new object type called detection, which contain queries or other actionable information that can identify an event or behavior.",
  "schema": "https://raw.githubusercontent.com/opencybersecurityalliance/stix-extensions/main/2.x/schemas/x-oca-detection.json",
  "version": "1.0.0",
  "extension_types": [
    "new-sdo"
  ]
}
```

## Examples

### Mail Client Opens Browser Detection

```json
    {
      "type": "x-oca-detection",
      "spec_version": "2.1",
      "id": "x-oca-detection--58834c29-4ceb-42a1-a218-336103021111",
      "created_by_ref": "identity--b085a68a-bf48-4316-9667-37af78cba894",
      "created": "2022-03-31T13:00:00.000Z",
      "modified": "2022-03-31T13:00:00.000Z",
      "name": "Process 1 - SpearPhish",
      "data_sources": [
        {
          "EventCode": "4688",
          "LogName": "Security",
          "TaskCategory": "Process Creation",
          "data_type": "WinEventLog:Security",
          "Creator_Process_Name": [
            "*outlook*",
            "*thunderbird*",
            "*mail*"
          ],
          "New_Process_Name": [
            "*edge*",
            "*chrome*",
            "*firefox*"
          ]
        }
      ],
      "analytic": {
        "rule":
"LS0tCnRpdGxlOiBTcGVhcnBoaXNoaW5nIHdpdGggTGluawppZDogc3BlYXJwaGlzaGluZwpzdGF0dXM6IGV4cGVyaW1lbnRhbApkZXNjcmlwdGlvbjogRGV0ZWN0cyBPZmZpY2UgbWFjcm8gb3BlbmluZyBmcm9tIGJyb3dzZXIuCnRhZ3M6Ci0gYXR0YWNrLmluaXRpYWxfYWNjZXNzCi0gYXR0YWNrLnQxNTY2LjAwMgphdXRob3I6IGRlbW8KZGF0ZTogMjAyMS8wNi8wNwpsb2dzb3VyY2U6CiAgcHJvZHVjdDogd2luZG93cwogIGluZGV4OiBtYWluCiAgY2F0ZWdvcnk6IHByb2Nlc3NfZXZlbnQKZGV0ZWN0aW9uOgogIHNlbGVjdGlvbjoKICAgIEV2ZW50Q29kZTogJzQ2ODgnCiAgICBDcmVhdG9yX1Byb2Nlc3NfTmFtZXxjb250YWluczoKICAgIC0gb3V0bG9vawogICAgLSB0aHVuZGVyYmlyZAogICAgLSBtYWlsCiAgICBOZXdfUHJvY2Vzc19OYW1lfGNvbnRhaW5zOgogICAgLSBlZGdlCiAgICAtIGNocm9tZQogICAgLSBmaXJlZm94CiAgY29uZGl0aW9uOiBzZWxlY3Rpb24KZmFsc2Vwb3NpdGl2ZXM6Ci0gTG93CmxldmVsOiBoaWdo",
        "type": "Sigma Rule - base64 encoded YAML file"
      },
      "extensions": {
        "extension-definition--c4690e13-107e-4796-8158-0dcf1ae7bc89": {
          "extension_type": "new-sdo"
        }
      }
    }

```

### Registry Value Modified Detection

```json
    {
      "type": "x-oca-detection",
      "spec_version": "2.1",
      "id": "x-oca-detection--458c02c9-3635-42e4-8873-6785e00517e7",
      "created_by_ref": "identity--b085a68a-bf48-4316-9667-37af78cba894",
      "created": "2022-03-31T13:00:00.000Z",
      "modified": "2022-03-31T13:00:00.000Z",
      "name": "Registry - Persistence",
      "data_sources": [
        {
          "EventCode": "4657",
          "LogName": "Security",
          "Message": "A registry value was modified.\n\nSubject:\n\tSecurity
ID:\t\tS-1-5-21-1102256457-2379380313-1247321256-500\n\tAccount Name:\t\tAdministrator\n\tAccount
Domain:\t\tSP17\n\tLogon ID:\t\t0x1A1ADFE8\n\nObject:\n\tObject
Name:\t\t\\REGISTRY\\MACHINE\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Run\n\tObject Value
Name:\tpersist\n\tHandle ID:\t\t0x918\n\tOperation Type:\t\tNew registry value created\n\nProcess
Information:\n\tProcess ID:\t\t0x18f0\n\tProcess
Name:\t\tC:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe\n\nChange
Information:\n\tOld Value Type:\t\t-\n\tOld Value:\t\t-\n\tNew Value Type:\t\tREG_SZ\n\tNew
Value:\t\tTrue",
          "TaskCategory": "Registry",
          "data_type": "WinEventLog:Security"
        }
      ],
      "analytic": {
        "rule":
"LS0tCnRpdGxlOiBSZWdpc3RyeSBSdW4gS2V5cwppZDogcmVnaXN0cnkgcGVyc2lzdGVuY2UKc3RhdHVzOiBleHBlcmltZW50YWwKZGVzY3JpcHRpb246IERldGVjdHMgbmV3IHJlZ2lzdHJ5IHJ1biBrZXkgY3JlYXRlZCBldmVudC4KdGFnczoKLSBhdHRhY2sucGVyc2lzdGVuY2UKLSBhdHRhY2sudDE1NDcKYXV0aG9yOiBkZW1vCmRhdGU6IDIwMjEvMDYvMDcKbG9nc291cmNlOgogIHByb2R1Y3Q6IHdpbmRvd3MKICBpbmRleDogbWFpbgogIGNhdGVnb3J5OiByZWdpc3RyeV9ldmVudApkZXRlY3Rpb246CiAgc2VsZWN0aW9uOgogICAgRXZlbnRDb2RlOiAnNDY1NycKICAgIE9iamVjdF9OYW1lfGNvbnRhaW5zOgogICAgLSBSdW4KICAgIC0gU2hlbGwgRm9sZGVycwogIGNvbmRpdGlvbjogc2VsZWN0aW9uCmZhbHNlcG9zaXRpdmVzOgotIEhpZ2gKbGV2ZWw6IGhpZ2g=",
        "type": "Sigma Rule - base64 encoded YAML file"
      },
      "extensions": {
        "extension-definition--c4690e13-107e-4796-8158-0dcf1ae7bc89": {
          "extension_type": "new-sdo"
        }
      }
    }
```
