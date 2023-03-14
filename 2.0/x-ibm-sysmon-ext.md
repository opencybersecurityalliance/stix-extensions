# Windows™ Sysmon extension
**Type Name**: `x-ibm-sysmon-ext`

The sysmon extension adds properties from the [sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon) event log which are not supported by the official stix definitions.

Due to the high relevance of these properties to threat detection and their popularity withing detection rules it is important to have a documented definition within stix to resolve these properties to.
These can than be used for example in order to translate [sigma rules](https://github.com/SigmaHQ/sigma) into stix.

| Property Name      | Type   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|--------------------|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| original_file_name | string | Specifies a PE original file name as extracted from the PE headers and is being parsed by sysmon as `OriginalFileName`. For further reading refer to this [blog](https://medium.com/@olafhartong/sysmon-10-0-new-features-and-changes-e82106f2e00). In short - an attacker may change the file name, but the name in the PE header will depict the original name. Editing the PE header will change the file hash as well which might have implications on detection evasion. This extension property should be added to the `file` sco is availbale. |

## Example:

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
                "type": "file",
                "name": "foo.exe",
                "hashes": {
                    "SHA-256": "effb46bba03f6c8aea5c653f9cf984f170dcdd3bbbe2ff6843c3e5da0e698766"
                },
                "extensions": {
                    "x-ibm-sysmon-ext": {
                        "original_file_name": "cmd.exe"
                    }
                }
            }
        }
}
```