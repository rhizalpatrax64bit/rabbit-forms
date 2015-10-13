# Html Field #

## Description ##

This field provides a full html wysiwog (What You See Is What You Got) editor to insert into form.

## External resources ##

The Html Field uses [TinyMCE](http://tinymce.moxiecode.com/) javascript library to build the html editor.

## Attributes ##

| **Attribute** | **Description** | **Example** |
|:--------------|:----------------|:------------|
| options       | One associative array containing the parameters to initialize the !TinyMCE editor, check the [configuration documentation](http://wiki.moxiecode.com/index.php/TinyMCE:Configuration) at [TinyMCE website](http://tinymce.moxiecode.com/) to get a complete list of avaliable options | _see below_ |

## Example ##

```
curriculum:
        type: Html
        label: Curriculum
        params:
            options:
                plugins: fullscreen,paste
                theme: advanced
                theme_advanced_toolbar_location: top
                theme_advanced_toolbar_align: left
                theme_advanced_buttons1_add: |,forecolor,fullscreen
                theme_advanced_buttons3: ''
```