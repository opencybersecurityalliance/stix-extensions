## process object with custom attributes

Specifies custom atributes for the [`process`](http://docs.oasis-open.org/cti/stix/v2.0/cs01/part4-cyber-observable-objects/stix-v2.0-cs01-part4-cyber-observable-objects.html#_Toc496716272) object to describe commonly used descriptors for a process.

| property name | type | description |
|--|--|--|
| x_window_title | `string` | Specifies the title of a process. This is some times the same as process name. Can also be different: for example a browser setting its title to the web page currently opened. |
| x_thread_id | `integer` | Specifies the id of the thread related to the process. For a multi-threaded process, this specifies the id of the first thread initialized by the process. |
| x_exit_code | `integer` | Specifies the exit code of a process. Present if this is a terminaton event. |
| x_uptime | `integer` | Specifies the amount of time in seconds a process has been up. |
| x_unique_id | `string` | Specifies globally unique identifier for a process, commonly used to mitigate PID reuse and to identify a specific process over time, across multiple monitored hosts.  For example - process-generated UUID, Sysmon Process GUIDs, or a hash of some uniquely identifying components of a process. |
| x_ttp_tags | `list` of type `string` | Specifies the list of keywords used to tag an event. |

Example:

    {
        "0": {
            "type": "process",
            "name": "services.exe",
            "pid": 1068,
            "x_unique_id": "{8dfc401c-1ef5-6175-0b00-000000001b00}",
            "binary_ref": "2",
            "command_line": "C:\\Windows\\system32\\services.exe"
        },
        "1": {
            "type": "process",
            "parent_ref": "0",
            "name": "svchost.exe",
            "pid": 2244,
            "cwd": "C:\\Windows\\system32\\",
            "x_unique_id": "{8dfc401c-1ef7-6175-2900-000000001b00}",
            "x_thread_id": "4242",
            "command_line": "C:\\Windows\\system32\\svchost.exe -k netsvcs -p -s Schedule",
            "x_ttp_tags": [
                "beats_input_codec_plain_applied"
            ]
        },
        "2": {
            "type": "file",
            "name": "services.exe",
            "parent_directory_ref": "3"
        },
        "3": {
            "type": "directory",
            "path": "C:\\Windows\\System32"
        }
    }
