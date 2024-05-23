## x-oca-coa-playbook-ext

Adds an extension to the `course-of-action` object to include references to related playbooks. The key for this extension when used in the extensions dictionary MUST be `extension-definition--bbc1d5c8-7ddc-4e89-be9c-f33ad02d71dd`.

| property name | type | description |
| -- | -- | -- |
| extension_type (required) | `string` | The value of this property MUST be property-extension.
| playbooks (required) | `dictionary` | The dictionary key is the UUID of a STIX 2.1 playbook object (as defined in section 2). The dictionary value is the playbook format (e.g., application/cacao+json, bpmn). When possible, this value SHOULD come from the values defined in the Template column of the IANA media type registry [Media Types]. For example, if a playbook is provided as an image in png format, the value following the IANA media type registry MUST be "image/png". Another example is CACAO security playbooks, where in [CACAO-Security-Playbooks-v2.0] Appendix C. IANA Considerations, the following media type is defined: "application/cacao+json"

## Extension Definition

```
{
    "type": "extension-definition",
    "spec_version": "2.1",
    "id": "extension-definition--bbc1d5c8-7ddc-4e89-be9c-f33ad02d71dd",
    "created_by_ref": "identity--b085a68a-bf48-4316-9667-37af78cba894",
    "created": "2022-03-31T13:00:00.000Z",
    "modified": "2024-05-16T12:44:08.273Z",
    "name": "x-oca-coa-playbook-ext Extension Definition",
    "description": "This definition extends the COA SDO with playbook references.",
    "schema": "https://raw.githubusercontent.com/opencybersecurityalliance/stix-extensions/main/playbook/schemas/x-oca-coa-playbook-ext.json",
    "version": "4.0.0",
    "extension_types": ["property-extension"]
}
```

## Example

### Quarantine and Remediate Course of Action with Playbook References

```
{
    "type": "course-of-action",
    "spec_version": "2.1",
    "id": "course-of-action--4e202c5a-c1df-42d8-9aef-809a8e172ae3",
    "created": "2022-03-31T13:00:00.000Z",
    "modified": "2024-05-16T12:44:08.273Z",
    "name": "Quarantine and remediate",
    "description": "Remediate by quarantining and performing analyst-guided steps",
    "extensions": {
        "extension-definition--bbc1d5c8-7ddc-4e89-be9c-f33ad02d71dd": {
            "extension_type": "property-extension",
            "playbooks": {
                "x-oca-playbook--9880df48-09a7-4e99-8070-0db8f4c946d0": "application/cacao+json",
                "x-oca-playbook--32f52089-9943-4231-bba3-5c02ba654755": "BPMN"
            }
        }
    }
}
```

## References

[CACAO-Security-Playbooks-v2.0]\
CACAO Security Playbooks Version 2.0. Edited by Bret Jordan and Allan Thomson. 27 November 2023. OASIS Committee Specification 01. https://docs.oasis-open.org/cacao/security-playbooks/v2.0/cs01/security-playbooks-v2.0-cs01.html. Latest version: https://docs.oasis-open.org/cacao/security-playbooks/v2.0/security-playbooks-v2.0.html.