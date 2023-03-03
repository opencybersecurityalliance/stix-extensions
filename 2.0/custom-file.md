## file object with custom attributes
Specifies custom atributes for the [`file`](http://docs.oasis-open.org/cti/stix/v2.0/cs01/part4-cyber-observable-objects/stix-v2.0-cs01-part4-cyber-observable-objects.html#_Toc496716232) object to describe commonly used descriptors for a file.

| property name | type | description |
|--|--|--|
| x_attributes | `list` of type `string` | Specifies an array of file attributes. Values may include archive, compressed, directory, encrypted, execute, hidden, read, readonly, system, write. |
| x_extension | `string` | Specifies the extension of the file, excluding the leading dot. example: png, gz |
| x_path | `string` | Specifies the full path to the file, including the file name. example: /home/alice/example.png |
| x_target_path | `string` | Specifies the target path for symbolic links. |
| x_type | `string` | Specifies the file type. File type can be file, directory, or symbolic link |
| x_unix | `dictionary` | Specifies the list of attributes associated with a unix file as a dictionary. Each dictionary key SHOULD come from the unix file vocabulary.  |
| x_owner_ref | `object-ref` | Specifies the ownership attributes of a file as a reference to a User Account Object. The object referenced in this property MUST be of type `user-account`. |
| x_win_drive_letter | `string` | Specifies the drive letter where the file is located on Windows. example C |
| x_pe | `dictionary` | Specifies the metadata of a portable executable file. Each dictionary key SHOULD come from the pe vocabulary. |
| x_code_signature | `dictionary` | Specifies metadata about the file signature. Each dictionary key SHOULD come from the code signature vocabulary. |

Unix file vocabulary
| value | type | description |
|--|--|--|
| device | `string` | Specifies the device that is the source of the file. example: sda |
| gid | `integer` | Specifies the primary group id of the file |
| group | `string` | Specifies the primary group name of the file |
| inode | `integer` | Specifies the inode representing the file in the filesystem. |
| mode | `integer` | Specifies the mode of the file in octal representation. |

PE vocabulary
| value | type | description |
|--|--|--|
| company | `string` | Specifies the internal company name of the file, provided at compile-time. example: Microsoft Corporation |
| description | `string` | Specifies the internal description of the file, provided at compile-time. example: Paint |
| file_version | `string` | Specifies the internal version of the file, provided at compile-time. example: 6.3.9600.17415 |
| original_file_name | `string` | Specifies the internal name of the file, provided at compile-time. example: MSPAINT.EXE |
| product | `string` | Specifies the internal product name of the file, provided at compile-time. example: Microsoft® Windows® Operating System |

Code signature vocabulary
| value | type | description |
|--|--|--|
| exists | `boolean` | Specifies the boolean to capture if a signature is present. |
| status | `string` | Specifies additional information about the certificate status. This is useful for logging cryptographic errors with the certificate validity or trust status. |
| subject_name | `string` | Specifies the subject name of the code signer. example: Microsoft Corporation |
| trusted | `boolean` | Specifies the trust status of the certificate chain. |
| valid | `boolean` | Specifies the boolean to capture if the digital signature is verified against the binary content. |

Example:

    {
        "5": {
            "type": "file",
            "x_pe": {
                "file_version": "10.0.17763.1 (WinBuild.160101.0800)",
                "product": "Microsoft\u00ae Windows\u00ae Operating System",
                "description": "Host Process for Windows Services",
                "company": "Microsoft Corporation",
                "original_file_name": "svchost.exe"
            },
            "name": "svchost.exe",
            "parent_directory_ref": "6",
            "hashes": {
                "SHA-256": "7fd065bac18c5278777ae44908101cdfed72d26fa741367f0ad4d02020787ab6",
                "MD5": "8a0a29438052faed8a2532da50455756"
            }
        },
        "6": {
            "type": "directory",
            "path": "C:\\Windows\\System32"
        }
    }
