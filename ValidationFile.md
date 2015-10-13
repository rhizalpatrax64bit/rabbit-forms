# File Validation #

## Description ##

This validation can validate information of files like the extension or size.

## Attributes ##

| **Attribute** | **Description** | **Example** |
|:--------------|:----------------|:------------|
| required      | If you set this attribute as true, the file will be required to be sent | true        |
| extensions    | This parameter accepts one array containing acceptable file extensions. Note: ever write the extensions lowercased | _see below_ |
| min\_size     | The minimal size of file (in bytes) | 2048        |
| max\_size     | The max size of file (in bytes) | 10240       |

## Example ##

This example demonstrate how to create a file validator to accepts only compressed files of at maximum 5mb of size.

```
fields:
    documents:
        label: Documents
        type: File
        validators:
            -type: File
             params:
                extensions:
                    -zip
                    -rar
                    -gz
                    -tz
                    -7z
                    -tar
                max_size: 5242880
```