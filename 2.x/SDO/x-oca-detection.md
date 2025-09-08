## x-oca-detection

Adds a new object for detecting adversary behaviors. STIX Indicators support the creation of
patterns to detect indicators of compromise. We wish to extend this to adversary behaviors using
Detection objects. For example, a Detection object for detecting the behavior of a mail client
opening a web browser may contain an analytic that matches the parent and child process names with
common mail clients and web browsers, respectively.

| property name            | type                       | description
|--------------------------|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| type (required)          | `string`                   | MUST be the literal "x-oca-detection"
| name (required)          | `string`                   | The name used to identify the Detection.
| analytic (required)      | `dictionary`               | Base64 encoded logic defining the detection along with the type of rule (e.g. Sigma rule).
| description              | `string`                   | Description of the detection.

## Extension Definition

```
{
  "type": "extension-definition",
  "spec_version": "2.1",
  "id": "extension-definition--c4690e13-107e-4796-8158-0dcf1ae7bc89",
  "created_by_ref": "identity--b085a68a-bf48-4316-9667-37af78cba894",
  "created": "2022-03-31T13:00:00.000Z",
  "modified": "2025-06-18T12:00:00.000Z",
  "name": "x-oca-detection Extension Definition",
  "description": "Detections contain logic to detect an adversary behavior.",
  "schema": "https://raw.githubusercontent.com/opencybersecurityalliance/stix-extensions/main/2.x/schemas/x-oca-detection.json",
  "version": "1.0.1",
  "extension_types": [
    "new-sdo"
  ]
}
```

## Examples

### Mail Client Opens Browser Detection

```
    {
      "type": "x-oca-detection",
      "spec_version": "2.1",
      "id": "x-oca-detection--58834c29-4ceb-42a1-a218-336103021111",
      "created_by_ref": "identity--b085a68a-bf48-4316-9667-37af78cba894",
      "created": "2022-03-31T13:00:00.000Z",
      "modified": "2025-06-06T17:08:00.000Z",
      "name": "Process 1 - SpearPhish",
      "description": "This detection checks for process creation events with EventCode 4688 where \"Creator_Process_Name\" contains a string associated with common email clients and \"New_Process_Name\" contains a string associated with common web browsers.",
      "analytic": {
        "rule": "LS0tCnRpdGxlOiBTcGVhcnBoaXNoaW5nIHdpdGggTGluawppZDogc3BlYXJwaGlzaGluZwpzdGF0dXM6IGV4cGVyaW1lbnRhbApkZXNjcmlwdGlvbjogRGV0ZWN0cyBPZmZpY2UgbWFjcm8gb3BlbmluZyBmcm9tIGJyb3dzZXIuCnRhZ3M6Ci0gYXR0YWNrLmluaXRpYWxfYWNjZXNzCi0gYXR0YWNrLnQxNTY2LjAwMgphdXRob3I6IGRlbW8KZGF0ZTogMjAyMS8wNi8wNwpsb2dzb3VyY2U6CiAgcHJvZHVjdDogd2luZG93cwogIGluZGV4OiBtYWluCiAgY2F0ZWdvcnk6IHByb2Nlc3NfZXZlbnQKZGV0ZWN0aW9uOgogIHNlbGVjdGlvbjoKICAgIEV2ZW50Q29kZTogJzQ2ODgnCiAgICBDcmVhdG9yX1Byb2Nlc3NfTmFtZXxjb250YWluczoKICAgIC0gb3V0bG9vawogICAgLSB0aHVuZGVyYmlyZAogICAgLSBtYWlsCiAgICBOZXdfUHJvY2Vzc19OYW1lfGNvbnRhaW5zOgogICAgLSBlZGdlCiAgICAtIGNocm9tZQogICAgLSBmaXJlZm94CiAgY29uZGl0aW9uOiBzZWxlY3Rpb24KZmFsc2Vwb3NpdGl2ZXM6Ci0gTG93CmxldmVsOiBoaWdo",
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

```
    {
      "type": "x-oca-detection",
      "spec_version": "2.1",
      "id": "x-oca-detection--458c02c9-3635-42e4-8873-6785e00517e7",
      "created_by_ref": "identity--b085a68a-bf48-4316-9667-37af78cba894",
      "created": "2022-03-31T13:00:00.000Z",
      "modified": "2025-06-06T17:08:00.000Z",
      "name": "Registry - Persistence",
      "description": "This detection checks for registry modification events with EventCode 4657 where \"Object_Name\" contains \"Run\" or \"Shell Folders\".",
      "analytic": {
        "rule": "LS0tCnRpdGxlOiBSZWdpc3RyeSBSdW4gS2V5cwppZDogcmVnaXN0cnkgcGVyc2lzdGVuY2UKc3RhdHVzOiBleHBlcmltZW50YWwKZGVzY3JpcHRpb246IERldGVjdHMgbmV3IHJlZ2lzdHJ5IHJ1biBrZXkgY3JlYXRlZCBldmVudC4KdGFnczoKLSBhdHRhY2sucGVyc2lzdGVuY2UKLSBhdHRhY2sudDE1NDcKYXV0aG9yOiBkZW1vCmRhdGU6IDIwMjEvMDYvMDcKbG9nc291cmNlOgogIHByb2R1Y3Q6IHdpbmRvd3MKICBpbmRleDogbWFpbgogIGNhdGVnb3J5OiByZWdpc3RyeV9ldmVudApkZXRlY3Rpb246CiAgc2VsZWN0aW9uOgogICAgRXZlbnRDb2RlOiAnNDY1NycKICAgIE9iamVjdF9OYW1lfGNvbnRhaW5zOgogICAgLSBSdW4KICAgIC0gU2hlbGwgRm9sZGVycwogIGNvbmRpdGlvbjogc2VsZWN0aW9uCmZhbHNlcG9zaXRpdmVzOgotIEhpZ2gKbGV2ZWw6IGhpZ2g=",
        "type": "Sigma Rule - base64 encoded YAML file"
      },
      "extensions": {
        "extension-definition--c4690e13-107e-4796-8158-0dcf1ae7bc89": {
          "extension_type": "new-sdo"
        }
      }
    }
```