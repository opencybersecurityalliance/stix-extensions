## windows-registry-key extension

Adds an extension to the windows-registry-key object to include references to related playbooks. The key for this extension when used in the extensions dictionary MUST be `extension-definition--2cf8c8c2-69f5-40f7-aa34-efcef2b912b1`.

| property name | type | description |
| -- | -- | -- |
| extension_type (required) | `string` | MUST be the literal "property-extension"
| operation_type | `string` | Operation performed on the registry key.
| user | `string` | User account associated with the process.
| computer | `string` | Computer hostname associated with the process.
| new_value | `string` | New value of the registry key if a change has been made.
| process_id | `string` | Process ID of the process that modified the registry.
| process_name | `string` | Name of the process that modified the registry.

## Extension Definition

```
{
  "type": "extension-definition",
  "spec_version": "2.1",
  "id": "extension-definition--2cf8c8c2-69f5-40f7-aa34-efcef2b912b1",
  "created_by_ref": "identity--b085a68a-bf48-4316-9667-37af78cba894",
  "created": "2022-03-31T13:00:00.000Z",
  "modified": "2022-03-31T13:00:00.000Z",
  "name": "x-oca-windows-registry-key Extension Definition",
  "description": "This schema extends the Windows Registry Key SCO.",
  "schema": "https://raw.githubusercontent.com/opencybersecurityalliance/oca-iob/main/apl_reference_implementation_bundle/revision_2/schemas/observables/extended-windows-registry-key.json",
  "version": "1.0.0",
  "extension_types": [
    "property-extension"
  ]
}
```

## Examples

### Windows Registry Key was Modified

```
{
  "type": "windows-registry-key",
  "spec_version": "2.1",
  "id": "windows-registry-key--c5a4244e-22d5-5797-8f78-c5fc3d1c0bde",
  "key": "\\REGISTRY\\MACHINE\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Run",
  "values": [
    {
      "name": "persist"
    }
  ],
  "extensions": {
    "extension-definition--2cf8c8c2-69f5-40f7-aa34-efcef2b912b1": {
      "operation_type": "modify",
      "new_value": "true",
      "process_id": "0x0",
      "process_name": "C:\\Windows\\regedit.exe",
      "extension_type": "property-extension"
    }
  }
}
```
