## x-oca-playbook

The current Course of Action object type in STIX 2.1 supports basic use cases such as sharing prose
courses of action but does not support the ability to represent structured and automated courses of
action, like orchestration workflows, or contain properties to represent metadata about courses of
action. Playbook objects encode such processes and may do so in various formats such as CACAO or
BPMN. The IOB Sub-Project wishes to thank Dr. Vasileios Mavroeidis and his teams at University of
Oslo / Cyentific AS for their technical discussions on best practices to represent CACAO playbooks
within STIX. Field names and descriptions from their playbook SDO specification document are used
here.

| property name            | type                       | description
|--------------------------|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| type (required)          | `string`                   | MUST be the literal "x-oca-playbook" |
| name (required)          | `string`                   | The name used to identify the Playbook. |
| description              | `string`                   | Description of the Playbook. |
| playbook_id              | `string`                   | A value that identifies the playbook. If the playbook itself includes a unique identifier (e.g., CACAO playbooks may include UUIDv4 or deterministic UUIDv5 identifiers), then playbook_id SHOULD use the same identifier for correlation purposes. Otherwise, the sharing entity MAY generate a UUIDv4 identifier. |
| playbook_format          | `string`                   | The standard/format/notation the playbook conforms to (e.g., CACAO, BPMN, Ansible). |
| playbook_type            | `list` of type `string`    | A list of playbook types that specifies the operational roles this playbook addresses. Each element SHOULD be from open vocab - playbook-type-ov. |
| playbook_bin             | `string`                   | The entire playbook encoded in base64. |
| playbook_abstraction     | `string`                   | The playbook’s level of abstraction. For example, a playbook can contain descriptions of processes for cybersecurity personnel or specific commands for an orchestrator to consume and execute. The value SHOULD come from open vocab playbook-abstraction-ov. |
| playbook_creation_time   | `timestamp`                | The time at which the first version of this playbook was created. The timestamp value MUST be precise to the nearest millisecond. |
| playbook_modification_time|`timestamp`                | The time that this particular version of this playbook was modified. The timestamp value MUST be precise to the nearest millisecond. |
| playbook_creator         | `object_ref`               | The identifier of the entity that created the playbook. |

## Playbook Type Vocabulary

Vocabulary Name: `playbook-type-ov`

An open vocabulary for the playbook_type field of a playbook object.

| vocabulary value | description |
|--|--|
| prevention | A playbook that is primarily focused on the orchestration steps required to prevent a known or expected security event, incident, or threat from occurring. |
| notification | A playbook that is primarily focused on the orchestration steps required to notify and disseminate information and other playbooks about a security event, incident, or threat. |
| detection | A playbook that is primarily focused on the orchestration steps required to detect a known security event, known or expected security-relevant activity, or for threat hunting. |
| investigation | A playbook that is primarily focused on the orchestration steps required to investigate what damage a security event, incident, or other security-relevant activity has caused. |
| mitigation | A playbook that is primarily focused on the orchestration steps required to mitigate a security event or incident that has occurred when remediation is not initially possible. |
| remediation | A playbook that is primarily focused on the orchestration steps required to remediate, resolve, or fix the resultant state of a security event or incident, and return the system, device, or network back to a nominal operating state. |
| analysis | As described in [NIST.SP.800-61r2]. |
| containment | As described in [NIST.SP.800-61r2]. |
| eradication | As described in [NIST.SP.800-61r2]. |
| recovery | As described in [NIST.SP.800-61r2]. |
| attack | A playbook that is primarily focused on the orchestration steps required to execute a penetration test or attack simulation to test or verify security controls or identify vulnerabilities within an organization’s environment. |

## Playbook Abstraction Vocabulary

Vocabulary Name: `playbook-abstraction-ov`

An open vocabulary for the playbook_abstraction field of a playbook object.

| value |  description |
|--|--|
| executable | An executable playbook is intended to be immediately actionable in an organization’s security infrastructure without requiring modification or updates to the workflow and commands. |
| template | A playbook template provides descriptions of actions related to a particular security incident, malware, vulnerability or other security operation. A template playbook will not be immediately executable by a receiving organization but may inform their own executable playbook for their specific environment or organization. |

## Extension Definition

```
{
  "type": "extension-definition",
  "spec_version": "2.1",
  "id": "extension-definition--809C4D84-7A6E-4039-97B4-DA9FEA03FCF9",
  "created_by_ref": "identity--b085a68a-bf48-4316-9667-37af78cba894",
  "created": "2022-03-31T13:00:00.000Z",
  "modified": "2022-03-31T13:00:00.000Z",
  "name": "x-oca-playbook Extension Definition",
  "description": "This schema creates a new object type called x-oca-playbook.",
  "schema": "https://raw.githubusercontent.com/opencybersecurityalliance/oca-iob/main/apl_reference_implementation_bundle/revision_2/schemas/sdos/playbook.json",
  "version": "1.0.0",
  "extension_types": [
    "new-sdo"
  ]
}
```

## Examples

### Quarantine and Remediate BPMN Playbook

```
{
  "type": "x-oca-playbook",
  "spec_version": "2.1",
  "id": "x-oca-playbook--32F52089-9943-4231-BBA3-5C02BA654755",
  "created": "2022-03-31T13:00:00.000Z",
  "modified": "2022-03-31T13:00:00.000Z",
  "name": "Quarantine and remediate",
  "playbook_id": "33624770-3AFE-4F63-8E63-F00915162F01",
  "description": "Remediate by quarantining and performing analyst guided steps. Optionally checks configuration management and attempts to automatically rebuild if necessary.",
  "playbook_format": "BPMN",
  "playbook_type": [
    "remediation"
  ],
  "playbook_bin": "PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPGJwbW46ZGVmaW5pdGlvbnMgeG1sbnM6YnBtbj0iaHR0cDovL3d3dy5vbWcub3JnL3NwZWMvQlBNTi8yMDEwMDUyNC9NT0RFTCIgeG1sbnM6YnBtbmRpPSJodHRwOi8vd3d3Lm9tZy5vcmcvc3BlYy9CUE1OLzIwMTAwNTI0L0RJIiB4bWxuczpkYz0iaHR0cDovL3d3dy5vbWcub3JnL3NwZWMvREQvMjAxMDA1MjQvREMiIHhtbG5zOnplZWJlPSJodHRwOi8vY2FtdW5kYS5vcmcvc2NoZW1hL3plZWJlLzEuMCIgeG1sbnM6ZGk9Imh0dHA6Ly93d3cub21nLm9yZy9zcGVjL0RELzIwMTAwNTI0L0RJIiB4bWxuczptb2RlbGVyPSJodHRwOi8vY2FtdW5kYS5vcmcvc2NoZW1hL21vZGVsZXIvMS4wIiBpZD0iRGVmaW5pdGlvbnNfMTN1dGs5YiIgdGFyZ2V0TmFtZXNwYWNlPSJodHRwOi8vYnBtbi5pby9zY2hlbWEvYnBtbiIgZXhwb3J0ZXI9IkNhbXVuZGEgTW9kZWxlciIgZXhwb3J0ZXJWZXJzaW9uPSI1LjUuMSIgbW9kZWxlcjpleGVjdXRpb25QbGF0Zm9ybT0iQ2FtdW5kYSBDbG91ZCIgbW9kZWxlcjpleGVjdXRpb25QbGF0Zm9ybVZlcnNpb249IjguMS4wIj4KICA8YnBtbjpwcm9jZXNzIGlkPSJQcm9jZXNzXzE4MTFmOHciIG5hbWU9IlN5c3RlbSBjb3Vyc2Ugb2YgYWN0aW9uIGFsZXJ0IiBpc0V4ZWN1dGFibGU9InRydWUiPgogICAgPGJwbW46c3RhcnRFdmVudCBpZD0iU3RhcnRFdmVudF8xIiBuYW1lPSJTeXN0ZW0gQ291cnNlIG9mIEFjdGlvbiBBbGVydCI+CiAgICAgIDxicG1uOm91dGdvaW5nPkZsb3dfMWoxZzdkaDwvYnBtbjpvdXRnb2luZz4KICAgIDwvYnBtbjpzdGFydEV2ZW50PgogICAgPGJwbW46c2VxdWVuY2VGbG93IGlkPSJGbG93XzFycXRpcmwiIHNvdXJjZVJlZj0iQWN0aXZpdHlfMGk5MWdlbiIgdGFyZ2V0UmVmPSJBY3Rpdml0eV8xamZ5ZzB5IiAvPgogICAgPGJwbW46c2VxdWVuY2VGbG93IGlkPSJGbG93XzFqMWc3ZGgiIHNvdXJjZVJlZj0iU3RhcnRFdmVudF8xIiB0YXJnZXRSZWY9IkFjdGl2aXR5XzF2djh5eXoiIC8+CiAgICA8YnBtbjpzZXJ2aWNlVGFzayBpZD0iQWN0aXZpdHlfMXZ2OHl5eiIgbmFtZT0iUXVhcmFudGluZSBzeXN0ZW0iPgogICAgICA8YnBtbjpleHRlbnNpb25FbGVtZW50cz4KICAgICAgICA8emVlYmU6dGFza0RlZmluaXRpb24gdHlwZT0iZWRyIiAvPgogICAgICA8L2JwbW46ZXh0ZW5zaW9uRWxlbWVudHM+CiAgICAgIDxicG1uOmluY29taW5nPkZsb3dfMWoxZzdkaDwvYnBtbjppbmNvbWluZz4KICAgICAgPGJwbW46b3V0Z29pbmc+Rmxvd18wZ2wxbnFvPC9icG1uOm91dGdvaW5nPgogICAgPC9icG1uOnNlcnZpY2VUYXNrPgogICAgPGJwbW46c2VydmljZVRhc2sgaWQ9IkFjdGl2aXR5XzBpOTFnZW4iIG5hbWU9IkNyZWF0ZSB0aWNrZXQiPgogICAgICA8YnBtbjpleHRlbnNpb25FbGVtZW50cz4KICAgICAgICA8emVlYmU6dGFza0RlZmluaXRpb24gdHlwZT0idGlja2V0aW5nIiAvPgogICAgICA8L2JwbW46ZXh0ZW5zaW9uRWxlbWVudHM+CiAgICAgIDxicG1uOmluY29taW5nPkZsb3dfMGdsMW5xbzwvYnBtbjppbmNvbWluZz4KICAgICAgPGJwbW46b3V0Z29pbmc+Rmxvd18xcnF0aXJsPC9icG1uOm91dGdvaW5nPgogICAgPC9icG1uOnNlcnZpY2VUYXNrPgogICAgPGJwbW46c2VydmljZVRhc2sgaWQ9IkFjdGl2aXR5XzFqZnlnMHkiIG5hbWU9IkNvbW1lbnQgaW4gdGlja2V0IHRoYXQgc3lzdGVtIGlzIHF1YXJhbnRpbmVkIj4KICAgICAgPGJwbW46ZXh0ZW5zaW9uRWxlbWVudHM+CiAgICAgICAgPHplZWJlOnRhc2tEZWZpbml0aW9uIHR5cGU9InRpY2tldGluZyIgLz4KICAgICAgPC9icG1uOmV4dGVuc2lvbkVsZW1lbnRzPgogICAgICA8YnBtbjppbmNvbWluZz5GbG93XzFycXRpcmw8L2JwbW46aW5jb21pbmc+CiAgICAgIDxicG1uOm91dGdvaW5nPkZsb3dfMDA3MjFoODwvYnBtbjpvdXRnb2luZz4KICAgIDwvYnBtbjpzZXJ2aWNlVGFzaz4KICAgIDxicG1uOnNlcXVlbmNlRmxvdyBpZD0iRmxvd18wMDcyMWg4IiBzb3VyY2VSZWY9IkFjdGl2aXR5XzFqZnlnMHkiIHRhcmdldFJlZj0iQWN0aXZpdHlfMTJsbjFvcyIgLz4KICAgIDxicG1uOnNlcXVlbmNlRmxvdyBpZD0iRmxvd18wZWFyMDg3IiBzb3VyY2VSZWY9IkFjdGl2aXR5XzEybG4xb3MiIHRhcmdldFJlZj0iQWN0aXZpdHlfMTUyNjY4biIgLz4KICAgIDxicG1uOnNlcXVlbmNlRmxvdyBpZD0iRmxvd18xY3NiMG9sIiBzb3VyY2VSZWY9IkFjdGl2aXR5XzE1MjY2OG4iIHRhcmdldFJlZj0iQWN0aXZpdHlfMHV2bWNuZSIgLz4KICAgIDxicG1uOnNlcnZpY2VUYXNrIGlkPSJBY3Rpdml0eV8wdXZtY25lIiBuYW1lPSJSZW1vdmUgcXVhcmFudGluZSBmcm9tIHN5c3RlbSI+CiAgICAgIDxicG1uOmV4dGVuc2lvbkVsZW1lbnRzPgogICAgICAgIDx6ZWViZTp0YXNrRGVmaW5pdGlvbiB0eXBlPSJlZHIiIC8+CiAgICAgIDwvYnBtbjpleHRlbnNpb25FbGVtZW50cz4KICAgICAgPGJwbW46aW5jb21pbmc+Rmxvd18xY3NiMG9sPC9icG1uOmluY29taW5nPgogICAgICA8YnBtbjpvdXRnb2luZz5GbG93XzFjZThxdWw8L2JwbW46b3V0Z29pbmc+CiAgICA8L2JwbW46c2VydmljZVRhc2s+CiAgICA8YnBtbjpzZW5kVGFzayBpZD0iQWN0aXZpdHlfMTJsbjFvcyIgbmFtZT0iU2VuZCBlbWFpbCB0byBTT0MgYW5hbHlzdCB0byByZXZpZXcgdGlja2V0Ij4KICAgICAgPGJwbW46ZXh0ZW5zaW9uRWxlbWVudHM+CiAgICAgICAgPHplZWJlOnRhc2tEZWZpbml0aW9uIHR5cGU9ImVtYWlsIiAvPgogICAgICA8L2JwbW46ZXh0ZW5zaW9uRWxlbWVudHM+CiAgICAgIDxicG1uOmluY29taW5nPkZsb3dfMDA3MjFoODwvYnBtbjppbmNvbWluZz4KICAgICAgPGJwbW46b3V0Z29pbmc+Rmxvd18wZWFyMDg3PC9icG1uOm91dGdvaW5nPgogICAgPC9icG1uOnNlbmRUYXNrPgogICAgPGJwbW46dXNlclRhc2sgaWQ9IkFjdGl2aXR5XzE1MjY2OG4iIG5hbWU9IlNPQyBhbmFseXN0IHJlc3RvcmVzIGFmZmVjdGVkIHN5c3RlbSI+CiAgICAgIDxicG1uOmluY29taW5nPkZsb3dfMGVhcjA4NzwvYnBtbjppbmNvbWluZz4KICAgICAgPGJwbW46b3V0Z29pbmc+Rmxvd18xY3NiMG9sPC9icG1uOm91dGdvaW5nPgogICAgPC9icG1uOnVzZXJUYXNrPgogICAgPGJwbW46c2VxdWVuY2VGbG93IGlkPSJGbG93XzFjZThxdWwiIHNvdXJjZVJlZj0iQWN0aXZpdHlfMHV2bWNuZSIgdGFyZ2V0UmVmPSJBY3Rpdml0eV8xdWZ1MGRzIiAvPgogICAgPGJwbW46c2VydmljZVRhc2sgaWQ9IkFjdGl2aXR5XzF1ZnUwZHMiIG5hbWU9IkNvbW1lbnQgaW4gdGlja2V0IHRoYXQgc3lzdGVtIGlzIHJlc3RvcmVkIGFuZCB0aGUgcXVhcmFudGluZSBpcyByZW1vdmVkIj4KICAgICAgPGJwbW46ZXh0ZW5zaW9uRWxlbWVudHM+CiAgICAgICAgPHplZWJlOnRhc2tEZWZpbml0aW9uIHR5cGU9InRpY2tldGluZyIgLz4KICAgICAgPC9icG1uOmV4dGVuc2lvbkVsZW1lbnRzPgogICAgICA8YnBtbjppbmNvbWluZz5GbG93XzFjZThxdWw8L2JwbW46aW5jb21pbmc+CiAgICAgIDxicG1uOm91dGdvaW5nPkZsb3dfMGgwc3RuYjwvYnBtbjpvdXRnb2luZz4KICAgIDwvYnBtbjpzZXJ2aWNlVGFzaz4KICAgIDxicG1uOnNlcXVlbmNlRmxvdyBpZD0iRmxvd18waDBzdG5iIiBzb3VyY2VSZWY9IkFjdGl2aXR5XzF1ZnUwZHMiIHRhcmdldFJlZj0iQWN0aXZpdHlfMDd2cmlleSIgLz4KICAgIDxicG1uOnNlcnZpY2VUYXNrIGlkPSJBY3Rpdml0eV8wN3ZyaWV5IiBuYW1lPSJDbG9zZSB0aWNrZXQiPgogICAgICA8YnBtbjpleHRlbnNpb25FbGVtZW50cz4KICAgICAgICA8emVlYmU6dGFza0RlZmluaXRpb24gdHlwZT0idGlja2V0aW5nIiAvPgogICAgICA8L2JwbW46ZXh0ZW5zaW9uRWxlbWVudHM+CiAgICAgIDxicG1uOmluY29taW5nPkZsb3dfMGgwc3RuYjwvYnBtbjppbmNvbWluZz4KICAgICAgPGJwbW46b3V0Z29pbmc+Rmxvd18wdmlqOHpnPC9icG1uOm91dGdvaW5nPgogICAgPC9icG1uOnNlcnZpY2VUYXNrPgogICAgPGJwbW46ZW5kRXZlbnQgaWQ9IkV2ZW50XzE3enBzbjUiPgogICAgICA8YnBtbjppbmNvbWluZz5GbG93XzB2aWo4emc8L2JwbW46aW5jb21pbmc+CiAgICA8L2JwbW46ZW5kRXZlbnQ+CiAgICA8YnBtbjpzZXF1ZW5jZUZsb3cgaWQ9IkZsb3dfMHZpajh6ZyIgc291cmNlUmVmPSJBY3Rpdml0eV8wN3ZyaWV5IiB0YXJnZXRSZWY9IkV2ZW50XzE3enBzbjUiIC8+CiAgICA8YnBtbjpzZXF1ZW5jZUZsb3cgaWQ9IkZsb3dfMGdsMW5xbyIgc291cmNlUmVmPSJBY3Rpdml0eV8xdnY4eXl6IiB0YXJnZXRSZWY9IkFjdGl2aXR5XzBpOTFnZW4iIC8+CiAgPC9icG1uOnByb2Nlc3M+CiAgPGJwbW5kaTpCUE1ORGlhZ3JhbSBpZD0iQlBNTkRpYWdyYW1fMSI+CiAgICA8YnBtbmRpOkJQTU5QbGFuZSBpZD0iQlBNTlBsYW5lXzEiIGJwbW5FbGVtZW50PSJQcm9jZXNzXzE4MTFmOHciPgogICAgICA8YnBtbmRpOkJQTU5TaGFwZSBpZD0iRXZlbnRfMTd6cHNuNV9kaSIgYnBtbkVsZW1lbnQ9IkV2ZW50XzE3enBzbjUiPgogICAgICAgIDxkYzpCb3VuZHMgeD0iMTQzMiIgeT0iMTEyIiB3aWR0aD0iMzYiIGhlaWdodD0iMzYiIC8+CiAgICAgIDwvYnBtbmRpOkJQTU5TaGFwZT4KICAgICAgPGJwbW5kaTpCUE1OU2hhcGUgaWQ9IkFjdGl2aXR5XzEwYXg2OXBfZGkiIGJwbW5FbGVtZW50PSJBY3Rpdml0eV8wN3ZyaWV5Ij4KICAgICAgICA8ZGM6Qm91bmRzIHg9IjEyODAiIHk9IjkwIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjgwIiAvPgogICAgICA8L2JwbW5kaTpCUE1OU2hhcGU+CiAgICAgIDxicG1uZGk6QlBNTlNoYXBlIGlkPSJBY3Rpdml0eV8wbDBhbjV1X2RpIiBicG1uRWxlbWVudD0iQWN0aXZpdHlfMXVmdTBkcyI+CiAgICAgICAgPGRjOkJvdW5kcyB4PSIxMTMwIiB5PSI5MCIgd2lkdGg9IjEwMCIgaGVpZ2h0PSI4MCIgLz4KICAgICAgPC9icG1uZGk6QlBNTlNoYXBlPgogICAgICA8YnBtbmRpOkJQTU5TaGFwZSBpZD0iQWN0aXZpdHlfMGtrZm11N19kaSIgYnBtbkVsZW1lbnQ9IkFjdGl2aXR5XzB1dm1jbmUiPgogICAgICAgIDxkYzpCb3VuZHMgeD0iOTkwIiB5PSI5MCIgd2lkdGg9IjEwMCIgaGVpZ2h0PSI4MCIgLz4KICAgICAgICA8YnBtbmRpOkJQTU5MYWJlbCAvPgogICAgICA8L2JwbW5kaTpCUE1OU2hhcGU+CiAgICAgIDxicG1uZGk6QlBNTlNoYXBlIGlkPSJBY3Rpdml0eV8wcGhhaDk1X2RpIiBicG1uRWxlbWVudD0iQWN0aXZpdHlfMTUyNjY4biI+CiAgICAgICAgPGRjOkJvdW5kcyB4PSI4NTAiIHk9IjkwIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjgwIiAvPgogICAgICA8L2JwbW5kaTpCUE1OU2hhcGU+CiAgICAgIDxicG1uZGk6QlBNTlNoYXBlIGlkPSJBY3Rpdml0eV8xZXNlZG1zX2RpIiBicG1uRWxlbWVudD0iQWN0aXZpdHlfMTJsbjFvcyI+CiAgICAgICAgPGRjOkJvdW5kcyB4PSI3MDAiIHk9IjkwIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjgwIiAvPgogICAgICA8L2JwbW5kaTpCUE1OU2hhcGU+CiAgICAgIDxicG1uZGk6QlBNTlNoYXBlIGlkPSJBY3Rpdml0eV8wMDFkaWQ1X2RpIiBicG1uRWxlbWVudD0iQWN0aXZpdHlfMWpmeWcweSI+CiAgICAgICAgPGRjOkJvdW5kcyB4PSI1NDAiIHk9IjkwIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjgwIiAvPgogICAgICA8L2JwbW5kaTpCUE1OU2hhcGU+CiAgICAgIDxicG1uZGk6QlBNTlNoYXBlIGlkPSJBY3Rpdml0eV8wc3dyeTU2X2RpIiBicG1uRWxlbWVudD0iQWN0aXZpdHlfMGk5MWdlbiI+CiAgICAgICAgPGRjOkJvdW5kcyB4PSIzODAiIHk9IjkwIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjgwIiAvPgogICAgICAgIDxicG1uZGk6QlBNTkxhYmVsIC8+CiAgICAgIDwvYnBtbmRpOkJQTU5TaGFwZT4KICAgICAgPGJwbW5kaTpCUE1OU2hhcGUgaWQ9IkFjdGl2aXR5XzA1eDZkOTNfZGkiIGJwbW5FbGVtZW50PSJBY3Rpdml0eV8xdnY4eXl6Ij4KICAgICAgICA8ZGM6Qm91bmRzIHg9IjIzMCIgeT0iOTAiIHdpZHRoPSIxMDAiIGhlaWdodD0iODAiIC8+CiAgICAgICAgPGJwbW5kaTpCUE1OTGFiZWwgLz4KICAgICAgPC9icG1uZGk6QlBNTlNoYXBlPgogICAgICA8YnBtbmRpOkJQTU5TaGFwZSBpZD0iX0JQTU5TaGFwZV9TdGFydEV2ZW50XzIiIGJwbW5FbGVtZW50PSJTdGFydEV2ZW50XzEiPgogICAgICAgIDxkYzpCb3VuZHMgeD0iMTQyIiB5PSIxMTIiIHdpZHRoPSIzNiIgaGVpZ2h0PSIzNiIgLz4KICAgICAgICA8YnBtbmRpOkJQTU5MYWJlbD4KICAgICAgICAgIDxkYzpCb3VuZHMgeD0iMTE2IiB5PSI4MiIgd2lkdGg9Ijg4IiBoZWlnaHQ9IjI3IiAvPgogICAgICAgIDwvYnBtbmRpOkJQTU5MYWJlbD4KICAgICAgPC9icG1uZGk6QlBNTlNoYXBlPgogICAgICA8YnBtbmRpOkJQTU5FZGdlIGlkPSJGbG93XzFycXRpcmxfZGkiIGJwbW5FbGVtZW50PSJGbG93XzFycXRpcmwiPgogICAgICAgIDxkaTp3YXlwb2ludCB4PSI0ODAiIHk9IjEzMCIgLz4KICAgICAgICA8ZGk6d2F5cG9pbnQgeD0iNTQwIiB5PSIxMzAiIC8+CiAgICAgIDwvYnBtbmRpOkJQTU5FZGdlPgogICAgICA8YnBtbmRpOkJQTU5FZGdlIGlkPSJGbG93XzFqMWc3ZGhfZGkiIGJwbW5FbGVtZW50PSJGbG93XzFqMWc3ZGgiPgogICAgICAgIDxkaTp3YXlwb2ludCB4PSIxNzgiIHk9IjEzMCIgLz4KICAgICAgICA8ZGk6d2F5cG9pbnQgeD0iMjMwIiB5PSIxMzAiIC8+CiAgICAgIDwvYnBtbmRpOkJQTU5FZGdlPgogICAgICA8YnBtbmRpOkJQTU5FZGdlIGlkPSJGbG93XzAwNzIxaDhfZGkiIGJwbW5FbGVtZW50PSJGbG93XzAwNzIxaDgiPgogICAgICAgIDxkaTp3YXlwb2ludCB4PSI2NDAiIHk9IjEzMCIgLz4KICAgICAgICA8ZGk6d2F5cG9pbnQgeD0iNzAwIiB5PSIxMzAiIC8+CiAgICAgIDwvYnBtbmRpOkJQTU5FZGdlPgogICAgICA8YnBtbmRpOkJQTU5FZGdlIGlkPSJGbG93XzBlYXIwODdfZGkiIGJwbW5FbGVtZW50PSJGbG93XzBlYXIwODciPgogICAgICAgIDxkaTp3YXlwb2ludCB4PSI4MDAiIHk9IjEzMCIgLz4KICAgICAgICA8ZGk6d2F5cG9pbnQgeD0iODUwIiB5PSIxMzAiIC8+CiAgICAgIDwvYnBtbmRpOkJQTU5FZGdlPgogICAgICA8YnBtbmRpOkJQTU5FZGdlIGlkPSJGbG93XzFjc2Iwb2xfZGkiIGJwbW5FbGVtZW50PSJGbG93XzFjc2Iwb2wiPgogICAgICAgIDxkaTp3YXlwb2ludCB4PSI5NTAiIHk9IjEzMCIgLz4KICAgICAgICA8ZGk6d2F5cG9pbnQgeD0iOTkwIiB5PSIxMzAiIC8+CiAgICAgIDwvYnBtbmRpOkJQTU5FZGdlPgogICAgICA8YnBtbmRpOkJQTU5FZGdlIGlkPSJGbG93XzFjZThxdWxfZGkiIGJwbW5FbGVtZW50PSJGbG93XzFjZThxdWwiPgogICAgICAgIDxkaTp3YXlwb2ludCB4PSIxMDkwIiB5PSIxMzAiIC8+CiAgICAgICAgPGRpOndheXBvaW50IHg9IjExMzAiIHk9IjEzMCIgLz4KICAgICAgPC9icG1uZGk6QlBNTkVkZ2U+CiAgICAgIDxicG1uZGk6QlBNTkVkZ2UgaWQ9IkZsb3dfMGgwc3RuYl9kaSIgYnBtbkVsZW1lbnQ9IkZsb3dfMGgwc3RuYiI+CiAgICAgICAgPGRpOndheXBvaW50IHg9IjEyMzAiIHk9IjEzMCIgLz4KICAgICAgICA8ZGk6d2F5cG9pbnQgeD0iMTI4MCIgeT0iMTMwIiAvPgogICAgICA8L2JwbW5kaTpCUE1ORWRnZT4KICAgICAgPGJwbW5kaTpCUE1ORWRnZSBpZD0iRmxvd18wdmlqOHpnX2RpIiBicG1uRWxlbWVudD0iRmxvd18wdmlqOHpnIj4KICAgICAgICA8ZGk6d2F5cG9pbnQgeD0iMTM4MCIgeT0iMTMwIiAvPgogICAgICAgIDxkaTp3YXlwb2ludCB4PSIxNDMyIiB5PSIxMzAiIC8+CiAgICAgIDwvYnBtbmRpOkJQTU5FZGdlPgogICAgICA8YnBtbmRpOkJQTU5FZGdlIGlkPSJGbG93XzBnbDFucW9fZGkiIGJwbW5FbGVtZW50PSJGbG93XzBnbDFucW8iPgogICAgICAgIDxkaTp3YXlwb2ludCB4PSIzMzAiIHk9IjEzMCIgLz4KICAgICAgICA8ZGk6d2F5cG9pbnQgeD0iMzgwIiB5PSIxMzAiIC8+CiAgICAgIDwvYnBtbmRpOkJQTU5FZGdlPgogICAgPC9icG1uZGk6QlBNTlBsYW5lPgogIDwvYnBtbmRpOkJQTU5EaWFncmFtPgo8L2JwbW46ZGVmaW5pdGlvbnM+Cg==",
  "playbook_abstraction": "template",
  "playbook_creation_time": "2022-03-31T13:00:00.000Z",
  "playbook_modification_time": "2022-03-31T13:00:00.000Z",
  "revoked": false,
  "playbook_creator": "identity--b085a68a-bf48-4316-9667-37af78cba894",
  "extensions": {
    "extension-definition--809C4D84-7A6E-4039-97B4-DA9FEA03FCF9": {
      "extension_type": "new-sdo"
    }
  }
}
```

### Quarantine and Remediate CACAO Playbook

```
{
  "type": "x-oca-playbook",
  "spec_version": "2.1",
  "id": "x-oca-playbook--9880DF48-09A7-4E99-8070-0DB8F4C946D0",
  "created": "2022-03-31T13:00:00.000Z",
  "modified": "2022-03-31T13:00:00.000Z",
  "name": "Quarantine and remediate",
  "description": "Remediate by quarantining and performing analyst guided steps. Optionally checks configuration management and attempts to automatically rebuild if necessary.",
  "playbook_id": "playbook--767d859e-7387-4e0c-95c0-458ca369486f",
  "playbook_format": "CACAO",
  "playbook_type": [
    "remediation"
  ],
  "playbook_bin": "ewogICJ0eXBlIjogInBsYXlib29rIiwKICAic3BlY192ZXJzaW9uIjogIjEuMCIsCiAgImlkIjogInBsYXlib29rLS03NjdkODU5ZS03Mzg3LTRlMGMtOTVjMC00NThjYTM2OTQ4NmYiLAogICJuYW1lIjogIlByb2Nlc3NfMTgxMWY4dzogUXVhcmFudGluZSBhbmQgUmVtZWRpYXRlIiwKICAiZGVzY3JpcHRpb24iOiAiIiwKICAicGxheWJvb2tfdHlwZXMiOiBbICJtaXRpZ2F0aW9uIiwgInJlbWVkaWF0aW9uIiBdLAogICJjcmVhdGVkX2J5IjogImlkZW50aXR5LS1iMDg1YTY4YS1iZjQ4LTQzMTYtOTY2Ny0zN2FmNzhjYmE4OTQiLAogICJjcmVhdGVkIjogIjIwMjItMDMtMzFUMTM6MDA6MDAuMDAwWiIsCiAgIm1vZGlmaWVkIjogIjIwMjItMDMtMzFUMTM6MDA6MDAuMDAwWiIsCiAgIndvcmtmbG93X3N0YXJ0IjogInN0YXJ0LS1lY2U1MzJkZi05NzBhLTQxN2MtYTEyNS01ZTc3MTNlMTBmN2MiLAogICJ3b3JrZmxvdyI6IHsKICAgICJzdGFydC0tZWNlNTMyZGYtOTcwYS00MTdjLWExMjUtNWU3NzEzZTEwZjdjIjogewogICAgICAidHlwZSI6ICJzdGFydCIsCiAgICAgICJuYW1lIjogIlN0YXJ0RXZlbnRfMTogU3lzdGVtIENvdXJzZSBvZiBBY3Rpb24gQWxlcnQiLAogICAgICAib25fY29tcGxldGlvbiI6ICJzaW5nbGUtLWQyMjQwOGZjLWE5OWMtNGM0NS04NzcwLTI3ZGFjNmRmMjkzYSIKICAgIH0sCiAgICAiZW5kLS00ZDMxMzRkOS02OGQyLTRiZGUtODdjYS1hNWJmZTg0NjhhYTYiOiB7CiAgICAgICJ0eXBlIjogImVuZCIsCiAgICAgICJuYW1lIjogIkV2ZW50XzE3enBzbjU6IEVuZCIKICAgIH0sCiAgICAic2luZ2xlLS1kMjI0MDhmYy1hOTljLTRjNDUtODc3MC0yN2RhYzZkZjI5M2EiOiB7CiAgICAgICJ0eXBlIjogInNpbmdsZSIsCiAgICAgICJuYW1lIjogIkFjdGl2aXR5XzF2djh5eXo6IFF1YXJhbnRpbmUgc3lzdGVtIiwKICAgICAgImNvbW1hbmRzIjogW3sKICAgICAgICAidHlwZSI6ICJodHRwLWFwaSIKICAgICAgfV0sCiAgICAgICJvbl9jb21wbGV0aW9uIjogInNpbmdsZS0tZDFkMTVhYjctYjU1Ny00ZjgyLThkOWItNDk1NDM4YTVjOWE5IgogICAgfSwKICAgICJzaW5nbGUtLWQxZDE1YWI3LWI1NTctNGY4Mi04ZDliLTQ5NTQzOGE1YzlhOSI6IHsKICAgICAgInR5cGUiOiAic2luZ2xlIiwKICAgICAgIm5hbWUiOiAiQWN0aXZpdHlfMGk5MWdlbjogQ3JlYXRlIHRpY2tldCIsCiAgICAgICJjb21tYW5kcyI6IFt7CiAgICAgICAgInR5cGUiOiAiaHR0cC1hcGkiCiAgICAgIH1dLAogICAgICAib25fY29tcGxldGlvbiI6ICJzaW5nbGUtLTNlZmJlMDU2LTZkMWUtNDQwNy04OWJiLWJiNTQwMTZkOWRlYSIKICAgIH0sCiAgICAic2luZ2xlLS0zZWZiZTA1Ni02ZDFlLTQ0MDctODliYi1iYjU0MDE2ZDlkZWEiOiB7CiAgICAgICJ0eXBlIjogInNpbmdsZSIsCiAgICAgICJuYW1lIjogIkFjdGl2aXR5XzFqZnlnMHk6IENvbW1lbnQgaW4gdGlja2V0IHRoYXQgc3lzdGVtIGlzIHF1YXJhbnRpbmVkIiwKICAgICAgImNvbW1hbmRzIjogW3sKICAgICAgICAidHlwZSI6ICJodHRwLWFwaSIKICAgICAgfV0sCiAgICAgICJvbl9jb21wbGV0aW9uIjogInNpbmdsZS0tMjdmODI3OGMtOGI4Ny00ODE1LThmNDAtOWM2YWY2MTAyMDNlIgogICAgfSwKICAgICJzaW5nbGUtLWZlYzU2ZDNkLTQ3YTQtNGY0Yi1hMGE3LWViNDI2OThjMWU4YiI6IHsKICAgICAgInR5cGUiOiAic2luZ2xlIiwKICAgICAgIm5hbWUiOiAiQWN0aXZpdHlfMHV2bWNuZTogUmVtb3ZlIHF1YXJhbnRpbmUgZnJvbSBzeXN0ZW0iLAogICAgICAiY29tbWFuZHMiOiBbewogICAgICAgICJ0eXBlIjogImh0dHAtYXBpIgogICAgICB9XSwKICAgICAgIm9uX2NvbXBsZXRpb24iOiAic2luZ2xlLS0zZjBlODNkYS01YzM3LTQ4MTYtOWQ4ZS03ZjU1ZWY0Yjc3YTQiCiAgICB9LAogICAgInNpbmdsZS0tM2YwZTgzZGEtNWMzNy00ODE2LTlkOGUtN2Y1NWVmNGI3N2E0IjogewogICAgICAidHlwZSI6ICJzaW5nbGUiLAogICAgICAibmFtZSI6ICJBY3Rpdml0eV8xdWZ1MGRzOiBDb21tZW50IGluIHRpY2tldCB0aGF0IHN5c3RlbSBpcyByZXN0b3JlZCBhbmQgdGhlIHF1YXJhbnRpbmUgaXMgcmVtb3ZlZCIsCiAgICAgICJjb21tYW5kcyI6IFt7CiAgICAgICAgInR5cGUiOiAiaHR0cC1hcGkiCiAgICAgIH1dLAogICAgICAib25fY29tcGxldGlvbiI6ICJzaW5nbGUtLWI3OTE4MTM0LTM4MDctNDQzMi1iNDdlLThhNGZlZjI2ODAzNSIKICAgIH0sCiAgICAic2luZ2xlLS1iNzkxODEzNC0zODA3LTQ0MzItYjQ3ZS04YTRmZWYyNjgwMzUiOiB7CiAgICAgICJ0eXBlIjogInNpbmdsZSIsCiAgICAgICJuYW1lIjogIkFjdGl2aXR5XzA3dnJpZXk6IENsb3NlIHRpY2tldCIsCiAgICAgICJjb21tYW5kcyI6IFt7CiAgICAgICAgInR5cGUiOiAiaHR0cC1hcGkiCiAgICAgIH1dLAogICAgICAib25fY29tcGxldGlvbiI6ICJlbmQtLTRkMzEzNGQ5LTY4ZDItNGJkZS04N2NhLWE1YmZlODQ2OGFhNiIKICAgIH0sCiAgICAic2luZ2xlLS03M2ZjYmVkNC0zOTNiLTRiY2QtODhlMi02OTMxNGM4ZTgyN2MiOiB7CiAgICAgICJ0eXBlIjogInNpbmdsZSIsCiAgICAgICJuYW1lIjogIkFjdGl2aXR5XzE1MjY2OG46IFNPQyBhbmFseXN0IHJlc3RvcmVzIGFmZmVjdGVkIHN5c3RlbSIsCiAgICAgICJjb21tYW5kcyI6IFt7CiAgICAgICAgInR5cGUiOiAibWFudWFsIgogICAgICB9XSwKICAgICAgIm9uX2NvbXBsZXRpb24iOiAic2luZ2xlLS1mZWM1NmQzZC00N2E0LTRmNGItYTBhNy1lYjQyNjk4YzFlOGIiCiAgICB9LAogICAgInNpbmdsZS0tMjdmODI3OGMtOGI4Ny00ODE1LThmNDAtOWM2YWY2MTAyMDNlIjogewogICAgICAidHlwZSI6ICJzaW5nbGUiLAogICAgICAibmFtZSI6ICJBY3Rpdml0eV8xMmxuMW9zOiBTZW5kIGVtYWlsIHRvIFNPQyBhbmFseXN0IHRvIHJldmlldyB0aWNrZXQiLAogICAgICAiY29tbWFuZHMiOiBbewogICAgICAgICJ0eXBlIjogImh0dHAtYXBpIgogICAgICB9XSwKICAgICAgIm9uX2NvbXBsZXRpb24iOiAic2luZ2xlLS03M2ZjYmVkNC0zOTNiLTRiY2QtODhlMi02OTMxNGM4ZTgyN2MiCiAgICB9CiAgfQp9Cg==",
  "playbook_abstraction": "template",
  "playbook_creation_time": "2022-03-31T13:00:00.000Z",
  "playbook_modification_time": "2022-03-31T13:00:00.000Z",
  "revoked": false,
  "playbook_creator": "identity--b085a68a-bf48-4316-9667-37af78cba894",
  "extensions": {
    "extension-definition--809C4D84-7A6E-4039-97B4-DA9FEA03FCF9": {
      "extension_type": "new-sdo"
    }
  }
}
```
