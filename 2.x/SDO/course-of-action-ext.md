## course-of-action extension

Adds an extension to the `course-of-action` object to include references to related playbooks. The key for this extension when used in the extensions dictionary MUST be `extension-definition--BBC1D5C8-7DDC-4E89-BE9C-F33AD02D71DD`.

| property name | type | description |
| -- | -- | -- |
| extension_type (required) | `string` | MUST be the literal "property-extension"
| playbooks | `dictionary` | The dictionary key is the format of the playbook (e.g. CACAO, BPMN). THe dictionary value is the STIX UUID of the associated x-oca-playbook object.

## Extension Definition

```
{
  "type": "extension-definition",
  "spec_version": "2.1",
  "id": "extension-definition--BBC1D5C8-7DDC-4E89-BE9C-F33AD02D71DD",
  "created_by_ref": "identity--b085a68a-bf48-4316-9667-37af78cba894",
  "created": "2022-03-31T13:00:00.000Z",
  "modified": "2022-03-31T13:00:00.000Z",
  "name": "x-oca-coa-playbook Extension Definition",
  "description": "This schema extends the Course of Action SDO with playbook information.",
  "schema": "https://raw.githubusercontent.com/opencybersecurityalliance/oca-iob/main/apl_reference_implementation_bundle/revision_2/schemas/sdos/course-of-action.json",
  "version": "1.0.0",
  "extension_types": [
    "property-extension"
  ]
}
```

## Example

### Quarantine and Remediate Course of Action with Playbook References

```
{
  "type": "course-of-action",
  "spec_version": "2.1",
  "id": "course-of-action--4E202C5A-C1DF-42D8-9AEF-809A8E172AE3",
  "created": "2022-03-31T13:00:00.000Z",
  "modified": "2022-03-31T13:00:00.000Z",
  "name": "Quarantine and remediate",
  "description": "Remediate by quarantining and performing analyst guided steps",
  "extensions": {
    "extension-definition--BBC1D5C8-7DDC-4E89-BE9C-F33AD02D71DD": {
      "extension_type": "property-extension",
      "playbooks": {
        "CACAO": "x-oca-playbook--9880DF48-09A7-4E99-8070-0DB8F4C946D0",
        "BPMN": "x-oca-playbook--32F52089-9943-4231-BBA3-5C02BA654755"
      }
    }
  }
}
```
