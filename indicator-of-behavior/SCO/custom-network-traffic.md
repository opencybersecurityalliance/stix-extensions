## network traffic object with custom attributes

Specifies custom atributes for the [`network`](https://docs.oasis-open.org/cti/stix/v2.1/os/stix-v2.1-os.html#_rgnc3w40xy) object to describe arbitrary network traffic that originates from a source and is addressed to a destination.

| property name | type | description |
|--|--|--|
| x_name | `string` | Specifies a name given by operators to sections of their network. |
| x_application | `string` | Specifies an identifiable application or service from network connection details. |
| x_direction | `string` | Specifies the direction of a network traffic from the host's point of view. Value must come from the Network Direction vocabulary |
| x_forwarded_ip | `object-ref` | Specifies the Host IP address when the source IP address is the proxy. Must be `ipv4-addr` or `ipv6-addr`. |
| x_community_id | `string` | Specifies a hash of source and destination IPs and ports, as well as the protocol used in a communication. |
| x_vlan | `dictionary` | Specifies information like interface number and name, vlan, and zone information to classify ingress traffic. Each dictionary key SHOULD come from the Network VLAN vocabulary. |

#### Network Direction Vocabluary

Vocabulary Name: `network-traffic-direction`

| Vocabulary Value | Description |
|--|--|
| `ingress` | Specifies inward traffic when mapping events from a host-based monitoring context. |
| `egress` | Specifies outward traffic when mapping events from a host-based monitoring context. |
| `inbound` | Specifies inward traffic when mapping events from a network or perimeter-based monitoring context. |
| `outbound` | Specifies outward traffic when mapping events from a network or perimeter-based monitoring context. |
| `internal` | Specifies the communication between two hosts within the perimeter. |
| `external` | Specifies the traffic between two hosts that are external to the perimeter. |
| `unknown` | Specifies unknown network traffic direction. |


#### VLAN Vocabluary

Vocabulary Name: `network-traffic-vlan`

| Vocabulary Value | type | Description |
|--|--|--|
| `id` | `string` | Specifies the reported VLAN ID. |
| `name` | `string` | Specifies the optional VLAN name. |
| `inner` | `object-ref` | Specifies the innermost VLAN when q-in-q VLAN tagging is present. Must be `network-traffic-vlan`. |

### Example

    {
        "0": {
            "type": "domain-name",
            "spec_version": "2.1",
            "id": "domain-name--3c10e93f-798e-5a26-a0c1-08156efab7f5",
            "value": "example.com"
        },
        "1": {
            "type": "network-traffic",
            "spec_version": "2.1",
            "id": "network-traffic--15a157a8-26e3-56e0-820b-0c2a8e553a2c",
            "dst_ref": "0",
            "protocols": [
                "ipv4",
                "tcp",
                "http"
            ],
            "x_name": "Guest_Wifi",
            "x_application": "twitter",
            "x_direction": "egress",
            "x_vlan": {
                "id": "1921",
                "name": "vlan1921",
                "inner": {
                    "id": "1250",
                    "name": "vlan1250"
                }
            }

        }
    }