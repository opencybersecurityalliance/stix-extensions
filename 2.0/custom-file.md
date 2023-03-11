## file object with custom attributes
Specifies custom atributes for the [`file`](https://docs.oasis-open.org/cti/stix/v2.1/os/stix-v2.1-os.html#_99bl2dibcztv) object to describe commonly used descriptors for a file.

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
| x_software_ref | `object-ref` | Specifies the the high level properties of a portable executable file. The object referenced in this property MUST be of type `software`.  |
| x_code_signature | `dictionary` | Specifies metadata about the file signature. Each dictionary key SHOULD come from the code signature vocabulary. |

### Unix file vocabulary
| value | type | description |
|--|--|--|
| device | `string` | Specifies the device that is the source of the file. example: sda |
| gid | `integer` | Specifies the primary group id of the file |
| group | `string` | Specifies the primary group name of the file |
| inode | `integer` | Specifies the inode representing the file in the filesystem. |
| mode | `integer` | Specifies the mode of the file in octal representation. |

### Code signature vocabulary
| value | type | description |
|--|--|--|
| exists | `boolean` | Specifies the boolean to capture if a signature is present. |
| status | `string` | Specifies additional information about the certificate status. This is useful for logging cryptographic errors with the certificate validity or trust status. |
| subject_name | `string` | Specifies the subject name of the code signer. example: Microsoft Corporation |
| trusted | `boolean` | Specifies the trust status of the certificate chain. |
| valid | `boolean` | Specifies the boolean to capture if the digital signature is verified against the binary content. |

Example:

    {
        "0": {
            "type": "file",
            "x_attributes": ["system"],
            "x_extension": "exe",
            "x_path": "C:\\Windows\\System32\\svchost.exe",
            "x_type": "file",
            "x_owner_ref": "3",
            "x_code_signature": {
                "exists": "true",
                "valid": "true"
            }
            "x_software_ref": "2",
            "name": "svchost.exe",
            "parent_directory_ref": "1",
            "hashes": {
                "SHA-256": "aaaa1111bbbb2222aaaa1111bbbb2222aaaa1111bbbb2222aaaa1111bbbb2222",
                "MD5": "00001111aaaa00001111aaaa00001111"
            }
        },
        "1": {
            "type": "directory",
            "path": "C:\\Windows\\System32"
        },
        "2": {
            "type": "software",
            "vendor": "Microsoft Corporation",
            "version": "10.0.17763.1 (WinBuild.160101.0800)",
            "name": "svchost.exe"
        },
        "3": {
            "type": "user-account",
            "user_id": "SYSTEM",
            "account_login": "SYSTEM"
        }
    }
