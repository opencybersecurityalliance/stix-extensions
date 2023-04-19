## x-ibm-finding object

The `x-ibm-finding` object describes a threat, policy, violation, or alert and its associated properties. 
Where possible, references are made to existing STIX objects (ie. ip addresses, users).


| Property Name | Type | Description |
|---------------|------|-------------|
| type (required) | `string` | The value of this property must be `x-ibm-finding`. |
| finding_type (required) | `string` | An open vocabulary that identifies the finding type. (ie. `threat`, `policy`, `violation`, `alert`.) |
| name (required) | `string` | The name of the threat, policy, violation, or  alert. |
| alert_id | `string` | The id of the finding from the data source |
| description | `string` | The description of the finding. |
| src_ip_ref | `object-ref` | Specifies the source ip address of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `ipv4-addr` or `ipv6-addr`. |
| dst_ip_ref | `object-ref` | Specifies the destination ip address of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `ipv4-addr` or `ipv6-addr`. |
| src_os_ref | `object-ref` | Specifies the source operating system of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `software`. |
| dst_os_ref | `object-ref` | Specifies the destination operating system of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `software`. |
| src_application_ref | `object-ref` | Specifies the source application of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `software`. |
| dst_application_ref | `object-ref` | Specifies the destination application of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `software`. |
| src_geolocation | `string` | Specifies the source geographic location of the finding. |
| dst_geolocation | `string` | Specifies the destination geographic location of the finding. |
| src_device | `string` | Specifies the source device of the finding. (ie. database, browser) |
| dst_device | `string` | Specifies the destination device of the finding. (ie. database, browser) |
| src_application_user_ref | `object-ref` | Specifies the source application user of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `user-account`. |
| dst_application_user_ref | `object-ref` | Specifies the destination application user of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `user-account`. |
| src_database_user_ref | `object-ref` | Specifies the source database user of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `user-account`. |
| dst_database_user_ref | `object-ref` | Specifies the destination database user of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `user-account`. |
| src_os_user_ref | `object-ref` | Specifies the source operating system user of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `user-account`. |
| dst_os_user_ref | `object-ref` | Specifies the destination operating system user of the finding, as a reference to the Cyber-observable Object. The object referenced must be of type `user-account`. |
| severity | `number` | Severity of the finding on a scale of 1-100. |
| confidence | `number` | Confidence of the finding on a scale of 1-100. |
| magnitude | `number` | Magnitude of the finding on a scale of 1-100. |
| rule_trigger_count | `number` | The number of rules that were triggered in the finding. |
| rule_names | `list` of type `string` | The rules that were triggered by the finding. |
| event_count | `number` | The number of events found in the finding. |
| time_observed | `timestamp` | The time in UTC when the finding was observed. |
| start | `timestamp` | The start time in UTC of the finding. |
| end | `timestamp` | The end time in UTC of the finding. |
| ttp_tagging_refs | `list` of type `identifier` | List of objects reffering to [x-ibm-ttp-tagging](x-ibm-ttp-tagging.md) describing techniques tactics and procedures mapped to this finding, such as MITRE ATT&CK TTP's |
| ioc_refs | `list` of type `object-ref` | References indicators of compromise related to this finding. Must be of type `file`, `ipv4-addr`, `ipv6-addr`, `domain`, `url` |

### Example:

```javascript
{
      "type": "observed-data",
      "id": "observed-data--ed82dd61-cc41-485b-b608-d278469e6259",
      "created_by_ref": "identity--33fa3e56-6511-40de-bc69-c5ffeb3838f9",
      "created": "2019-07-18T19:11:07.537Z",
      "modified": "2019-07-18T19:11:07.537Z",
      "first_observed": "2019-07-18T19:06:20.459257Z",
      "last_observed": "2019-07-18T19:08:10.111663Z",
      "number_observed": 1,
      "objects": {
        "0": {
          "type": "ipv4-addr",
          "value": "127.0.0.1"
        },
        "1": {
          "type": "ipv4-addr",
          "value": "192.168.0.12"
        },
        "2": {
          "type": "user-account",
          "user_id": "danny.elliott@ibm.com"
        },
        "3": {
          "type": "software",
          "name": "Windows",
          "version": "10.0"
        },
        "4": {
          "type": "x-ibm-finding",
          "name": "Some rule name",
          "finding_type": "violation",
          "time_observed": "2019-07-18T19:06:20.459257Z",
          "severity": 80,
          "src_ip_ref": "0",
          "dst_ip_ref": "1",
          "src_application_user_ref": "2",
          "src_application_ref": "3",
          "src_geolocation": "USA",
          "src_device": "Chrome",
          "ttp_tagging_refs": [5], 
          "ioc_refs": ["6","7"]
       },
       "5": {
          "type": "x-ibm-ttp-tagging",
          "name": "Active Scanning",
          "url": "https://attack.mitre.org/versions/v8/techniques/T1595/",
          "confidence": 0.8,
          "kill_chain_phases": [
             {
                "kill_chain_name": "mitre-attack",
                "phase_name": "reconnaissance"
             }
          ],
          "extensions": 
          {
             "mitre-attack-ext": 
             {
                "tactic_id": "TA0043",
                "tactic_url": "https://attack.mitre.org/versions/v8/tactics/TA0043/",
                "tactic_name": "Reconnaissance",
                "technique_id": "T1595",
                "technique_url": "https://attack.mitre.org/versions/v8/techniques/T1595/",
                "technique_name": "Active Scanning"
             }
          }
        },
        "6": {
                "type": "ipv4-addr",
                "value": "13.14.1.1"
             },
        "7": {
                "type": "url",
                "value": "http://maliciousmalware.bad"
        }
    }
}
```
