## process extension

Adds an extension to the process object to include references to related playbooks. The key for this extension when used in the extensions dictionary MUST be `extension-definition--f9dbe89c-0030-4a9d-8b78-0dcd0a0de874`.

| property name | type | description |
| -- | -- | -- |
| extension_type (required) | `string` | MUST be the literal "property-extension"
| operation_type | `string` | Operation associated with the process.
| computer | `string` | Computer hostname associated with the process.
| name | `string` | Process names or REGEX pattern to match against.
| win_event_code | `string` | Windows Event Code number.
| creator_user | `string` | User account associated with the process.

## Extension Definition

```
{
  "type": "extension-definition",
  "spec_version": "2.1",
  "id": "extension-definition--f9dbe89c-0030-4a9d-8b78-0dcd0a0de874",
  "created_by_ref": "identity--b085a68a-bf48-4316-9667-37af78cba894",
  "created": "2022-03-31T13:00:00.000Z",
  "modified": "2022-03-31T13:00:00.000Z",
  "name": "x-oca-process Extension Definition",
  "description": "This schema extends the Process SCO with additional Windows Event Log fields.",
  "schema": "https://raw.githubusercontent.com/opencybersecurityalliance/oca-iob/main/apl_reference_implementation_bundle/revision_2/schemas/observables/extended-process.json",
  "version": "1.0.0",
  "extension_types": [
    "property-extension"
  ]
}
```

## Examples

### Email Client Process Created

```
{
  "type": "process",
  "spec_version": "2.1",
  "id": "process--862e625d-48bb-489e-8d4e-f7d8cd2fcaaa",
  "is_hidden": false,
  "pid": 0,
  "cwd": "C:\\Program Files\\Microsoft Office\\Office14\\",
  "command_line": "C:\\Program Files\\Microsoft Office\\Office14\\OUTLOOK.EXE",
  "extensions": {
    "extension-definition--f9dbe89c-0030-4a9d-8b78-0dcd0a0de874": {
      "extension_type": "property-extension",
      "operation_type": "created",
      "name": "OUTLOOK.EXE",
      "win_event_code": "4688"
    }
  },
  "created_time": "2022-03-31T13:00:00.000Z",
  "defanged": false
}
```

### Outlook Email Client Opens Chrome Web Browser

```
{
  "type": "process",
  "spec_version": "2.1",
  "id": "process--862e625d-48bb-489e-8d4e-f7d8cd2fcbbb",
  "is_hidden": false,
  "pid": 0,
  "cwd": "C:\\Program Files\\Microsoft Office\\Office14\\",
  "command_line": "C:\\User\\jsmith.CBIS\\AppData\\Local\\Google\\Chrome\\Application\\chrome.exe --single-argument https://172.25.1.19/download/test.docm",
  "parent_ref": "process--862e625d-48bb-489e-8d4e-f7d8cd2fcaaa",
  "extensions": {
    "extension-definition--f9dbe89c-0030-4a9d-8b78-0dcd0a0de874": {
      "extension_type": "property-extension",
      "operation_type": "created",
      "name": chrome.exe",
      "win_event_code": "4688"
    }
  },
  "created_time": "2022-03-31T13:00:00.000Z",
  "defanged": false
}
```
