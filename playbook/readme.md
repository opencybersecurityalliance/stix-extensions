# Playbook Extension

The current STIX 2.1 Course of Action object type supports basic use cases such as sharing prose courses of action. This specification extends STIX 2.1 with one new SDO and a property extension for the Course of Action SDO for sharing automated courses of action (i.e., orchestration workflows or playbooks).

## course-of-action Playbook Extension

Adds an extension to the course-of-action object to include references to related playbooks.

**Extension Definition:** [extension-definition/extension-definition--bbc1d5c8-7ddc-4e89-be9c-f33ad02d71dd.json](./extension-definition/extension-definition--bbc1d5c8-7ddc-4e89-be9c-f33ad02d71dd.json)

**Schema:** [schemas/x-oca-coa-playbook-ext.json](./schemas/x-oca-coa-playbook-ext.json)

### Example

-   Quarantine and Remediate Course of Action with Playbook References: [examples/course-of-action--4e202c5a-c1df-42d8-9aef-809a8e172ae3.json](./examples/course-of-action--4e202c5a-c1df-42d8-9aef-809a8e172ae3.json)

## x-oca-playbook

The properties comprising the Playbook SDO are defined below.

**Extension Definition:** [extension-definition/extension-definition--809c4d84-7a6e-4039-97b4-da9fea03fcf9.json](./extension-definition/extension-definition--809c4d84-7a6e-4039-97b4-da9fea03fcf9.json)

**Schema:** [schemas/x-oca-playbook.json](./schemas/x-oca-playbook.json)

### Examples

-   Quarantine and Remediate BPMN Playbook: [examples/x-oca-playbook--32f52089-9943-4231-bba3-5c02ba654755.json](./examples/x-oca-playbook--32f52089-9943-4231-bba3-5c02ba654755.json)

-   Quarantine and Remediate CACAO Playbook: [examples/x-oca-playbook--9880df48-09a7-4e99-8070-0db8f4c946d0.json](examples/x-oca-playbook--9880df48-09a7-4e99-8070-0db8f4c946d0.json)
