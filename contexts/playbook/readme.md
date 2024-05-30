# Open Cybersecurity Alliance Playbook Extension

The current STIX 2.1 Course of Action object type supports basic use cases such as sharing prose courses of action. This specification extends STIX 2.1 with one new SDO and a property extension for the Course of Action SDO for sharing automated courses of action (i.e., orchestration workflows or playbooks) [STIX2.1-COA-Playbook-Extension].

Full specification: [STIX2.1_COA_Playbook_Extension_v4](./STIX2.1_COA_Playbook_Extension_v4.asciidoc)

## Overview

The STIX x-oca-playbook SDO allows the inclusion of playbooks in STIX CTI. The playbooks may be represented using existing specifications such as Collaborative Automated Course of Action Operations (CACAO) and Business Process Model and Notation (BPMN), or other more custom variants such as PowerPoint, JPEG, SVG, PDF, text documents, and many more. \
x-oca-playbook SDOs may then be referenced in the extended STIX Course of Action SDO that allows for the sharing of the attached playbooks.

## x-oca-coa-playbook-ext

Adds an extension to the STIX Course of Action object to include references to related playbooks.

**Extension Definition:** [extension-definition--bbc1d5c8-7ddc-4e89-be9c-f33ad02d71dd.json](./../../2.x/extension-definitions/extension-definition--bbc1d5c8-7ddc-4e89-be9c-f33ad02d71dd.json)

**Schema:** [x-oca-coa-playbook-ext.json](./../../2.x/schemas/x-oca-coa-playbook-ext.json)

### Example

-   Quarantine and Remediate Course of Action with Playbook References: [course-of-action--4e202c5a-c1df-42d8-9aef-809a8e172ae3.json](./examples/course-of-action--4e202c5a-c1df-42d8-9aef-809a8e172ae3.json)

## x-oca-playbook

The properties comprising the Playbook SDO are defined below.

**Extension Definition:** [extension-definition--809c4d84-7a6e-4039-97b4-da9fea03fcf9.json](./../../2.x/extension-definitions/extension-definition--809c4d84-7a6e-4039-97b4-da9fea03fcf9.json)

**Schema:** [x-oca-playbook.json](./../../2.x/schemas/x-oca-playbook.json)

### Examples

-   Quarantine and Remediate BPMN Playbook: [examples/x-oca-playbook--32f52089-9943-4231-bba3-5c02ba654755.json](./examples/x-oca-playbook--32f52089-9943-4231-bba3-5c02ba654755.json)

-   Quarantine and Remediate CACAO Playbook: [examples/x-oca-playbook--9880df48-09a7-4e99-8070-0db8f4c946d0.json](examples/x-oca-playbook--9880df48-09a7-4e99-8070-0db8f4c946d0.json)

## References

**[STIX2.1-COA-Playbook-Extension]** \
_Playbook SDO and Course of Action Property Extensions Version 4.0 for STIX™ Version 2.1_. Edited by OCA IOB Sub-Project Security Playbooks Working Group. 17 May 2024. OASIS Open Cyber Security Alliance Specification. Latest stage: https://docs.google.com/document/d/1mjFhYK_fLKzKK9X5qstoZkRF7GNTLiwM/

**[CACAO-Security-Playbooks-v2.0]** \
_CACAO Security Playbooks Version 2.0_. Edited by Bret Jordan and Allan Thomson. 27 November 2023. OASIS Committee Specification 01. https://docs.oasis-open.org/cacao/security-playbooks/v2.0/cs01/security-playbooks-v2.0-cs01.html. Latest version: https://docs.oasis-open.org/cacao/security-playbooks/v2.0/security-playbooks-v2.0.html.
