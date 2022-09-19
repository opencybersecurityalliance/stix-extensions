## x-oca-event
Adds a new object for describing events. 
Since STIX was originally created for threat intelligence and not for SIEM or EDR data, it did not have the concept of an event.
Take an endpoint file create event as an example - the observed data would include the process and file details - but you would be missing the context
to underdstand what happened between these two - did the process create or delete or write to the file?
Another example is a cross process event. You would have details of two processes - but you wouldnt know which process performed the cross process event on the other.
The `x-oca-event` object adds this context. What action was performed, Where was it performed, what was the outcome and what are the references to other SCO's that this event relates to.
Use of references helps to hint the relevance of the data. For example an file create event should have the `x-oca-event.file_ref` pointing to the created file. This would help the observer undersdtand, since a typical observed data SDO would contain more than one `file` SCO.

| property name | type | description |
|--|--|--|
|type| `string` | x-oca-event |
|action|`string`|describes the event action. for example process create|
|category|`list` of type `string`|categories describing the event. for example "process" or "system"|
|code|`integer`|event code or event id from the original log source|
|created|`timestamp`|when this event was created|
|start|`timestamp`|when this event started|
|end|`timestamp`|when this event ended|
|duration|`integer`|the duration of this event from start to end in nanoseconds|
|module|`string`|Name of the module this data is coming from. for example "sysmon"|
|original_ref|`object-ref`|references the original raw event data. must be of type `artifact`|
|outcome|`string`|the outcome of this event. for example "process create success"|
|provider|`string`|the provider of this log. for example "Microsoft Windows Security Event Log"|
|agent|`string`|describes the name of the agent that collected this event log|
|host_ref|`object-ref`|references the host related to this event. must be of type `x-oca-asset`|
|url_ref|`object-ref`|references a url related to this event. must be of type `url`|
|file_ref|`object-ref`|references a file related to this event. must be of type `file`|
|process_ref|`object-ref`|references a process related to this event. must be of type `process`|
|parent_process_ref|`object-ref`|references a parent process related to this event. must be of type `process`|
|cross_process_target_ref|`object-ref`|references the target process in case of a cross process event. must be of type `process`|
|domain_ref|`object-ref`|references a domain related to this event. must be of type `domain-name`|
|registry_ref|`object-ref`|references windows registry data related to this event. must be of type `windows-registry-key`|
|network_ref|`object-ref`|references network traffic related to this event. must be of type `network-traffic`|
|ip_refs|`list` of type `object-ref`|references any ip addresses related to this event. must be of type `ipv4-address` or `ipv6-address`|
|user_ref|`object-ref`|references the user related to this event. must be of type `user-account`|
| severity | `number` | Severity of the event on a scale of 1-100. | 
| start | `timestamp` | The start time in UTC of the event. |
| end | `timestamp` | The end time in UTC of the event. |
| timezone | `string` | The timezone where the event was discovered. |
| duration | `string` | The duration of the event. |
| dataset | `string` | The dataset of the event. |

## Examples

### an event indicating a network communication from an endpoint

network communication from the host `host1.exmaple.com` to url `https://example.com/download` performed by the `chrome.exe` process.

```
{
        "id": "observed-data--7805aca6-b29d-4e1a-86b2-ba4eb1110051",
        "type": "observed-data",
        "created_by_ref": "identity--ab920cb1-239b-4371-b7f6-66f634de9927",
        "created": "2022-07-15T18:42:31.000Z",
        "modified": "2022-07-15T18:42:31.000Z",
        "first_observed": "2022-07-15T18:42:31.000Z",
        "last_observed": "2022-07-15T18:42:31.000Z",
        "number_observed": 1,
        "objects":
        {
            "0":
            {
                "type": "x-oca-event",
                "action": "Network Connection Created",
                "created": "2022-07-15T18:42:31.000Z",
                "host_ref": "1",
                "provider": "EDR",
                "original_ref": "4",
                "user_ref": "5",
                "process_ref": "8",
                "network_ref": "10",
                "url_ref": "11",
                "domain_ref": "13"
            },
            "1":
            {
                "type": "x-oca-asset",
                "ip_refs": ["3"],
                "hostname": "host1.example.com",
                "mac_refs": ["2"]
            },
            "2":
            {
                "type": "mac-addr",
                "value": "12:34:56:78:9a:bc"
            },
            "3":
            {
                "type": "ipv4-addr",
                "value": "192.0.2.0"
            },
            "4":
            {
                "type": "artifact",
                "payload_bin": "[original event log data base 64 encoded]"
            },
            "5":
            {
                "type": "user-account",
                "user_id": "S-1-2-3-4",
                "account_login": "joe@example.com"
            },
            "6":
            {
                "name": "chrome.exe",
                "type": "file",
                "hashes":
                {
                    "SHA-1": "114c52257780067e3f8bfab4d2706be6debc0ace"
                },
                "parent_directory_ref": "7"
            },
            "7":
            {
                "path": "C:\\Program Files\\Google\\Chrome\\Application",
                "type": "directory"
            },
            "8":
            {
                "pid": 14068,
                "name": "chrome.exe",
                "type": "process",
                "created": "2022-07-15T15:41:11.3214492Z",
                "command_line": "C:\\Program Files\\Google\\Chrome\\Application\\chrome.exe --disable-features --enable-features",
                "creator_user_ref": "5",
                "parent_ref": "9",
                "binary_ref": "6"
            },
            "9":
            {
                "pid": 7116,
                "name": "explorer.exe",
                "type": "process",
                "created": "2022-07-15T08:01:20.813Z",
                "creator_user_ref": "5"
            },
            "10":
            {
                "type": "network-traffic",
                "src_ref": "3",
                "dst_ref": "12",
                "src_port": 2041,
                "dst_port": 443,
                "protocols": ["tcp", "https"]
            },
            "11":
            {
                "type": "url",
                "value": "https://example.com/download"
            },
            "12":
            {
                "type": "ipv6-addr",
                "value": "2001:db8::"
            },
            "13":
            {
                "type": "domain-name",
                "value": "example.com"
            }
        }
    }
```


### an event indicating a file create from an endpoint

A file `example.exe` has been created on the host `host1.exmaple.com` by the `chrome.exe` process.

```
{
        "id": "observed-data--7805aca6-b29d-4e1a-86b2-ba4eb1110046",
        "type": "observed-data",
        "created_by_ref": "identity--ab920cb1-239b-4371-b7f6-66f634de9927",
        "created": "2022-07-15T18:43:10.813Z",
        "modified": "2022-07-15T18:43:10.813Z",
        "first_observed": "2022-07-15T18:43:10.813Z",
        "last_observed": "2022-07-15T18:43:10.813Z",
        "number_observed": 1,
        "objects":
        {
            "0":
            {
                "type": "x-oca-event",
                "action": "FileCreated",
                "created": "2022-07-15T18:43:21.3214492Z",
                "file_ref": "10",
                "host_ref": "1",
                "provider": "EDR",
                "original_ref": "5",
                "user_ref": "5",
                "process_ref": "8"
            },
            "1":
            {
                "type": "x-oca-asset",
                "ip_refs": ["3"],
                "hostname": "host1.example.com",
                "mac_refs": ["2"]
            },
            "2":
            {
                "type": "mac-addr",
                "value": "12:34:56:78:9a:bc"
            },
            "3":
            {
                "type": "ipv4-addr",
                "value": "192.0.2.0"
            },
            "4":
            {
                "type": "artifact",
                "payload_bin": "[original event log data base 64 encoded]"
            },
            "5":
            {
                "type": "user-account",
                "user_id": "S-1-2-3-4",
                "account_login": "joe@example.com"
            },
            "6":
            {
                "name": "chrome.exe",
                "type": "file",
                "hashes":
                {
                    "SHA-1": "114c52257780067e3f8bfab4d2706be6debc0ace"
                },
                "parent_directory_ref": "7"
            },
            "7":
            {
                "path": "C:\\Program Files\\Google\\Chrome\\Application",
                "type": "directory"
            },
            "8":
            {
                "pid": 14068,
                "name": "chrome.exe",
                "type": "process",
                "created": "2022-07-15T15:41:11.3214492Z",
                "command_line": "C:\\Program Files\\Google\\Chrome\\Application\\chrome.exe --disable-features --enable-features",
                "creator_user_ref": "5",
                "parent_ref": "9",
                "binary_ref": "6"
            },
            "9":
            {
                "pid": 7116,
                "name": "explorer.exe",
                "type": "process",
                "created": "2022-07-15T08:01:20.813Z",
                "creator_user_ref": "5"
            },
            "10":
            {
                "type": "file",
                "name": "example.exe",
                "parent_directory_ref": "11",
                "hashes":
                {
                    "SHA-1": "223c52257780067e3f8bfab4d2706be6debc0aca"
                }
            },
            "11":
            {
                "type": "directory",
                "path": "C:\\Users\\joe\\Downloads"
            }
        }
    }
```

## IAM Extension

**Type Name**: `x-iam-ext`

The IAM extension represents data from Identity and Access Management events. The key for this extension when used in the **extensions** dictionary **MUST** be `x-iam-ext`. An object using the IAM Extension **MUST** contain at least one property from this extension.

| property name | type | description |
|--|--|--|
| result| `string` | Result of the action such as "success" or "failure" |
| sub_category| `string` | Identity source type used for authentication: clouddirectory, oidc,saml, ibmldap, maasconnect etc. |
| realm | `string` | Identity source of user. Examples: <ul> <li>Cloud Directory: CloudIdentityRealm </li> <li> IBMid: www.ibm.com </li> <li>SAML Enterprise: AzureRealm </li> <li> LDAP Pass-Through: www.cloudsecurity.com </li><li> OIDC: www.yahoo.com </li> |
| application_id | `string` | Identifier of application that caused event to be generated |
| user_id | `string` | Identifier of user that caused event to be generated  |
| application_type | `string` |  Type of application such as Custom application or specific cloud application |
| browser_agent | `string` |  Browser user agent |
| application_name | `string` | Name of application that caused event to be generated |
| cause | `string` |  The message describing the result of action |
| messageid | `string` |  The messageid for the message in cause  |
| target | `string` |  Target of the event  |
| targetid | `string` |  Supplemental information to define the target of the action. Used by resources: user, group  |
| targetid_realm | `string` |  realm of the target. Used by resources: user, group  |
| targetid_username | `string` |  User name of the target. Used by resources: user, group  |
| deleted | `string` |   For the resource group, number of users deleted |
| performedby_clientname | `string` |  API client name  |
| performedby_realm | `string` |   realm of the person who performed the action.  |
| performedby_username | `string` |  User name  of the person who performed the action.  |
| continent_name | `string` |  Geoip information for IP address - Continent name  |
| country_iso_code | `string` |  Geoip information for IP address - Country code  |
| country_name | `string` |  Geoip information for IP address - Country name  |
| city_name | `string` |  Geoip information for IP address - City name  |
| policy_action | `string` |  Action related to policy such as Block, MFA, Allow   |
| policy_name | `string` |  The policy name that were applied to the event.  |
| rule_name | `string` |  Name of the rule that got triggerd for risk based authentication  |
| decision_reason | `string` |  Decision reason for policy action  |
| location_lat | `string` | Geoip information for IP address - Location Lattitude  |
| location_lon | `string` |  Geoip information for IP address - Location Longitude |
| risk_level | `string` |  Level of risk -  Very high, High, Medium, Low |
| risk_score | `string` | Risk Score  |
| deviceid | `string` |   Identifier for device |
| is_device_compliant | `string` | Boolean flag to indicate if device is compliant  |
| is_device_managed | `string` |  Boolean flag to indicate if device is managed |
| mdm_customerid | `string` | Customer id for MDM (Mobile Device Managent)  |

### Example

	{
            "id": "observed-data--47418fa7-6edd-4406-88be-13fe5cfd4f08",
            "type": "observed-data",
            "created_by_ref": "32a23267-52fb-4e82-859b-0a15d6a2d334",
            "created": "2022-03-23T06:08:05.058Z",
            "modified": "2022-03-23T06:08:05.058Z",
            "objects": {
                "0": {
                    "type": "x-oca-event",
                    "extensions": {
                        "x-iam-ext": {
                            "continent_name": "Asia",
                            "city_name": "Kolkata",
                            "country_iso_code": "IN",
                            "country_name": "India",
                            "cause": "Successful login",
                            "browser_agent": "PAN GlobalProtect/5.2.10-6 (Microsoft Windows 10 Enterprise , 64-bit) Mozilla/5.0 (Windows NT 6.2; Win64; x64; Trident/7.0; rv:11.0) like Gecko",
                            "target": "https://login.w3.ibm.com/saml/sps/auth?stateid=6f738328-b096-4252-8186-b18b8e5559ee",
                            "subcategory": "federation",
                            "realm": "www.ibm.com",
                            "location_lon": "88.3832",
                            "location_lat": "22.518"
                        }
                    },
                    "ip_refs": [
                        "1"
                    ],
                    "outcome": "success",
                    "action": "authentication_login",
                    "agent": "oidc",
                    "user_ref": "2",
                    "category": "authentication",
                    "provider": "IBM Security Verify Event",
                    "domain_ref": "3",
                    "module": "authbroker",
                    "created": "2022-03-21T06:14:48.458Z"
                },
                "1": {
                    "type": "ipv4-addr",
                    "value": "223.233.24.47"
                },
                "2": {
                    "type": "user-account",
                    "account_type": "oidc",
                    "account_login": "user@ibm.com"
                },
                "3": {
                    "type": "domain-name",
                    "value": "isrras.ice.ibmcloud.com"
                }
            },
            "first_observed": "2022-03-23T06:08:05.058Z",
            "last_observed": "2022-03-23T06:08:05.058Z",
            "number_observed": 1
        }
