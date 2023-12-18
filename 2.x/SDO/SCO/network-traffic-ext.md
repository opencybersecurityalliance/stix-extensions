## network-traffic extension

Adds an extension to the network-traffic object to contain RITA beacon information. The key for this extension when used in the extensions dictionary MUST be `extension-definition--3b7505ce-2a18-496e-aa58-311dac6c1473`.

| property name | type | description |
| -- | -- | -- |
| extension_type (required) | `string` | MUST be the literal "property-extension"
| connections | `integer` | Number of connections reported by RITA.
| score | `float` | Beaconing score reported by RITA.
| computer | `string` | Computer hostname associated with the process.

## Extension Definition

```
{
  "type": "extension-definition",
  "spec_version": "2.1",
  "id": "extension-definition--3b7505ce-2a18-496e-aa58-311dac6c1473",
  "created_by_ref": "identity--b085a68a-bf48-4316-9667-37af78cba894",
  "created": "2022-03-31T13:00:00.000Z",
  "modified": "2022-03-31T13:00:00.000Z",
  "name": "x-oca-network-traffic Extension Definition",
  "description": "This schema extends the Network Traffic SCO with beacon scoring information from Real Intelligence Threat Analytics (RITA).",
  "schema": "https://raw.githubusercontent.com/opencybersecurityalliance/oca-iob/main/apl_reference_implementation_bundle/revision_2/schemas/observables/extended-network-traffic.json",
  "version": "1.0.0",
  "extension_types": [
    "property-extension"
  ]
}
```

## Example

```
{
  "type": "network-traffic",
  "spec_version": "2.1",
  "id": "network-traffic--15a157a8-26e3-56e0-820b-0c2a8e553a2c",
  "src_ref": "ipv4-addr--57a33521-9761-54a9-81de-3c11e441d86b",
  "src_port": 443,
  "dst_ref": "ipv4-addr--bba1d187-08fb-5000-aed1-ef055c1dfd24",
  "dst_port": 443,
  "protocols": [
    "ipv4",
    "tcp",
    "http",
    "https"
  ],
  "extensions": {
    "extension-definition--3b7505ce-2a18-496e-aa58-311dac6c1473": {
      "connections": 4022,
      "score": 0.834,
      "extension_type": "property-extension"
    }
  }
}
```
