## High Value Target Tool extension

High Value Targets (HVTs) are applications, their underlying information
systems, and data for which unauthorized access, use, disclosure,
disruption, modification, or destruction could cause a significant
impact to an organization's ability to perform its mission or conduct
business.

The IoB HVT extension empowers defenders to share detailed information
about software abuse cases, track threat actor patterns more accurately,
and chart attack flows regarding legitimate software as an adversarial
target. This enables threat-informed leaders and cyber risk personnel to
assess and quantify cyber risks associated with targeted software,
allowing for the development of more precise defensive strategies.

High Value Target is an open concept for the community to use. More information about the High Value Target concept is available at [https://www.highvaluetarget.org](https://www.highvaluetarget.org/).

An extension is added to the `tool` object to include High Value Target
information. The key for this extension when used in the extensions
dictionary MUST be
`extension-definition--fb58a27d-32d2-4b8d-9705-e3cfd2d3dcdf`.

  | property name                | type                  | description                                                                                                      |
  |------------------------------| ----------------------| -----------------------------------------------------------------------------------------------------------------|
  | extension_type (required)    | `string`              | MUST be the literal "property-extension"                                                                         |
  | high_value_target_attributes | `array` of `string`   |  Array of high value target attributes. Elements SHOULD come from the open vocab high-value-target-attribute-ov. |

### Tool Type Open Vocabulary Additions

The tool-type-ov describes categories of tools that can be used to
perform attacks. The following additional values are added to
tool-type-ov.

  
  | value                      | description                                                                                                                                                                             |
  |----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
  | hypervisors-virtualization | Tools used to virtualize execution of commands or operating systems with direct access and control to underlying hardware, such as VDI or containers.                                   |
  | identity-access-management | Tools used to store secrets that can be stolen or abused, such as corporate directories, PKI etc.                                                                                       |
  | security-monitoring        | Tools used to provide the defender the ability to monitor for malicious behaviors, such as SIEM or SOAR tools.                                                                          |
  | backup-storage             | Tools used to create copies and transfer data stored on endpoints or other devices, such as NAS, recovery managers, remote or local storage.                                            |
  | endpoint-management        | Tools used for remote endpoint administration, update and configuration such as patches management or asset inventory.                                                                  |
  | endpoint-security          | Tools used to protect the endpoints, contribute to the secure operation of the endpoint or collect information such as antimalware or EDR.                                              |
  | network-management         | Tools used to manage systems or networks which can provide an adversary visibility into the management control plane, such as DNS, network configuration or traffic monitoring systems. |
  | network-security           | Tools used to prevent malicious network traffic from entering or leaving a segment or boundary, such as NAC, firewall or NIPS.                                                          |
  | office-productivity        | Tools used to collaborate, communicate or share unstructured data such as email, file sharing and meeting platforms.                                                                    |
  | crisis-management          | Tools used to allow defenders to communicate during an incident (in-band or out-of-band) and can provide adversary with visibility of defensive tactics and crisis recovery plans.      |
  | business-data-repository   | Tools used to enable the business to deliver the organization's mission and/or store highly valuable or large amount of data, such as ERP, critical business applications or databases. |

### High Value Target Attribute Open Vocabulary

The high-value-target-attribute-ov open vocabulary describes attributes
of high value target tools when weaponized by an adversary.

  | value                | description                                                                                                                                       |
  |----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
  | tamper-prone         | The adversary leverages functionality or configuration that is prone to be weaponized in support of further malicious actions.                    |
  | internal-prospecting | The adversary leverages functionality to manage distributed systems or networks which provides visibility into the management control plane.      |
  | stores-secrets       | The adversary leverages access to stored secrets that can be stolen or abused.                                                                    |
  | stealthiness         | The adversary leverages functionality that provides the ability to bypass detection mechanisms and protection safeguards.                         |
  | external-exposure    | The adversary leverages external network exposure to pivot from untrusted to trusted networks.                                                    |
  | infiltrate-comms     | The adversary leverages functionality that enables defenders to communicate (in-band or out-of-band) and gains visibility into defensive tactics. |
  | blindside-defense    | The adversary leverages functionality that directly targets and impairs the defender's investigative and detective capabilities.                  |
  | inhibit-restoration  | The adversary leverages functionality that can permanently damage backup and restore capabilities.                                                |
  | stores-data          | The adversary leverages functionality that allows access to highly valuable or large amount of data.                                              |
  | widespread-presence  | The adversary leverages widely implemented and inherently trusted tools to maximize their presence and impact.                                    |
 
## Extension Definition
```
    {
      "type": "extension-definition",
      "spec_version": "2.1",
      "id": "extension-definition--fb58a27d-32d2-4b8d-9705-e3cfd2d3dcdf",
      "created_by_ref": "identity--b085a68a-bf48-4316-9667-37af78cba894",
      "created": "2022-03-31T13:00:00.000Z",
      "modified": "2022-03-31T13:00:00.000Z",
      "name": "High Value Target Tool Extension Definition",
      "description": "This schema extends the Tool SDO with High Value Target information.",
      "schema": "TBD",
      "version": "1.0.0",
      "extension_types": [
        "property-extension"
      ]
    }
```
## Example

```
    {
      "type": "tool",
      "spec_version": "2.1",
      "id": "tool--d22c9169-f725-4760-a801-4dfc4d1c2676",
      "created": "2022-03-31T13:00:00.000Z",
      "modified": "2022-03-31T13:00:00.000Z",
      "name": "ACME database",
      "description": "Database used to store enterprise logs and metrics.",
      "tool_types": ["business-data-repository"],
      "extensions": {
        "extension-definition--fb58a27d-32d2-4b8d-9705-e3cfd2d3dcdf": {
          "extension_type": "property-extension",
          "high_value_target_attributes": ["stores-data"]
        }
      }
    }
```
