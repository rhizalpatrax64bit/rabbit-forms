# TextBox Field #

## Description ##

This field provides text box input, at start it can be a simple text box but i put some add attributes that can make this a little bit better. Check this out!

Since Rabbit Forms Beta 1.0.5 the textbox field automatic apply the htmlentities method into passed values before insert then into database to prevent user to send html, you can set the attribute **accept\_html** to true to disable this feature.

## External resources ##

The masked input resource javascript is provided by [digitalBush Masked Input Plugin](http://digitalbush.com/projects/masked-input-plugin)

The watermark input resource javascript is provided by [digitalBush Watermark Input Plugin](http://digitalbush.com/projects/watermark-input-plugin)

Thanks for coders of these great libraries :)

## Attributes ##

| **Attribute** | **Description** | **Example** |
|:--------------|:----------------|:------------|
| class         | This attribute defines a class to be added to textbox html | inputClass  |
| style         | This attribute defines a inline style to be added to textbox html | width: 300px; |
| mode          | This attribute is used when you want to use text box as password field, when you put password in this attribute the user input will me not readable and when the form refill fields this field will not be refilled | password    |
| mask          | This is one killer feature, by simple adding this attribute you can created masked text box input, to know about how to use mask patterns check at [plugin page](http://digitalbush.com/projects/masked-input-plugin) | 99/99/9999  |
| watermark     | This attribute provide a way to add a simple watermark to field, know more at [plugin page](http://digitalbush.com/projects/watermark-input-plugin) | Enter your login here |
| accept\_html  | Set this attribute to true to disable the auto html filter feature | true        |

## Examples ##

See below some examples of textbox field usage:

_simple usage_
```
name:
    type: TextBox
    label: Name
```

_using as password_
```
password:
    type: TextBox
    label: Password
    params:
        mode: password
```

_using a time mask with watermark_
```
time:
    type: TextBox
    label: Initial time
    params:
        mask: 99:99:99
        watermark: hh:mm:ss
```