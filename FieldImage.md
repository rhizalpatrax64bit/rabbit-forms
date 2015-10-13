# Image Field #

## Description ##

This field is an extension of [File](FieldFile.md) field, but this field has some helpers to image files. This field automatic insert a file validation to accept only image file types, and you can do resize operations on images direct from configuration without any code, and when you are retrieving data, this fields will display a image into retrieve instead only the name of file.

## External resources ##

To do resize operations on images this field users [ImageToolbox](http://image-toolbox.sourceforge.net/) library.

## Attributes ##

| **Attribute** | **Description** | **Example** |
|:--------------|:----------------|:------------|
| class         | This attribute defines a class to be added to file html | inputClass  |
| style         | This attribute defines a inline style to be added to file html | width: 300px; |
| resize\_mode  | This attribute defines the mode of resize operation, see the options in the modes table below. | crop        |
| resize\_width | The width of new image | 300         |
| resize\_height | The height of new image | 200         |
| resize\_bgcolor | This attribute sets the background color to fill if you are using preserve mode (the default color is black) | #000000     |
| copies        | This attribute is used to make copies of image (see below) | _see below_ |
| display\_copy | This attribute defines a image copy to be used when retrieving the image field, the value of this attribute is the label of copy (if this attribute is not set, the original image will be displayed) | thumbnail   |

notes:
  1. if you don't set any resize attribute the image  will be saved with original size
  1. you can send only resize\_width or resize\_height, in this case the script will automatic calculate the other dimension to maintain image aspect ratio

## Resize Modes ##

The following table describes the available resize modes.

| **Mode** | **Description** |
|:---------|:----------------|
| fix      | This is the default mode, the image will be resized exactly with the size defined, if it's out of ratio the image will be distorted |
| crop     | In this mode, if the new size is out of base image ratio, the image will be cropped as necessary and will lose some parts but without distorted |
| preserve | In this mode, if the new size is out of base image ratio, the image will be reduced and fit inside of new size box and the remaining space will be filled with a background color |

## Copies ##

In many ways you will need some copies of image into server, for example, you can save the image with original size and create one thumbnail with a reduced version of image, to do this the Image Field provides a way to create many copies with many different sizes.

The copies configuration is one list with many copies configurations, the attributes to configure a copy is the same **resize** attributes as normal image, and the copy has one additional attribute called **label** that can be used to distinct the copies.

## Example ##

This example demonstrate how to use Image Field.

```
photo:
  type: Image
  label: User Photo
  params:
    resize_width: 640
    copies:
      -label: thumbnail
       resize_width: 100
       resize_height: 100
       resize_mode: crop
    display_copy: thumbnail
```