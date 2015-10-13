# Configuration #

Rabbit Forms is a high customizable library, and the configuration is the soul to make this real. If you has read the quick start, you see a little about this. Good, let's take it in order.

## Configuration Array ##

The configuration is nothing more than an n-leveled array, but to work it needs to follow a pattern, let's the skeleton of configuration pattern:

```
table: table_name
primary_key: primary_key_of_table
form:
    prechange: preChangeCallback
    validation: functionValidation
    type: formtype
    hidden:
        hiddenField: value
        anotherHidden: value
    automatic_assets: true
    view:
        template: template_view
        params:
            param1: value
            param2: value
fields:
    field_name:
        type: FieldType
        label: Field Label
        value: defaultValue
        persist: true
        params:
            param1: value
            param2: value
        validators:
            - type: Validator1
              params:
                  validator1_param1: value
            - type: Validator2
    anotherField:
        type: Type
        label: Label
retrieve:
    orderby: name
    pagination:
        base_url: controller/base/
        per_page: 10
    filters:
        -name like 'a%'
        -price > 30
    manage: controller/method/
    delete: controller/method/
    fields:
        -field_name
        -anotherField
    view:
        template: retrieve_view
        params:
            param1: value
            param2: value
```

Wow!! Is big!

The data above is in YAML way, and demonstrate all possibilities to create a configuration, yet, you don't need to use all this in your configuration. You can create configurations using PHP arrays to, like:

```
$config = array(
    'table' => 'myTable',
    'primary_key' => 'primary_key',
    'fields' => array(
        'field_name' => array(
            'type' => 'FieldType',
            'label' => 'FieldLabel'
        )
    )
);
```

I think you understand. In most cases you will use an YAML file to create configuration (because you write to less using) but you can use configuration arrays to create a more dynamic configuration.

Let's see what is the base configuration data:

| **Configuration** | **Description** | **Required** |
|:------------------|:----------------|:-------------|
| table             | the table that will be used to make CRUD | true         |
| primary\_key      | the primary key field of table, this will be used to edit and other internal things | false        |
| form              | this configuration maintain the form configuration, see more bellow | false        |
| fields            | this maintains fields configuration, see more bellow | true         |
| retrieve          | this maintains the retrieval configuration (more bellow too =P) | true         |

## Form Configuration ##

The form configuration defines the form behavior, the properties to configure is:

| **Configuration** | **Description** | **Required** |
|:------------------|:----------------|:-------------|
| type              | This property defines form class to use to manager form, in most cases you don't need to change this because default form class can supply many cases, but if you need a form level validation or do custom operations you will extend the form class to wherever you want | false        |
| hidden            | This property set hidden fields to pass into form, you can define how many hidden fields you want | false        |
| automatic\_assets | This property defines if form load the assets of fields automatic, if you set this property to false, you will need to manually load assets (scripts and styles) to fields that need them | false        |
| view              | This property configures the view of form (the template to display data), read more at view configuration | false        |
| validation        | This property accepts one string containing a callback function to be called to validate form at all, this function needs to be defined in the currect CodeIgniter control and returns true if the form is valid and false otherwise, the callback function may have this signature: **public function my\_validator(Rabbit\_Form $form)**. If the form fails, to send a message to user, use this: **$form->setValidationMessage('user message')**| false        |
| preinsert         | This property accepts one string containing a callback function to be called to do any operation before insert a new record, this function needs to be defined into current CodeIgniter controller | false        |
| postinsert        | This property accepts one string containing a callback function to be called to do any operation after insert a new record, this function needs to be defined into current CodeIgniter controller | false        |
| preupdate         | This property accepts one string containing a callback function to be called to do any operation before update a record, this function needs to be defined into current CodeIgniter controller | false        |
| postupdate        | This property accepts one string containing a callback function to be called to do any operation after update a record, this function needs to be defined into current CodeIgniter controller | false        |
| prechange         | This property accepts one string containing a callback function to be called to do any operation before change a record (this is fired on insert and update), this function needs to be defined into current CodeIgniter controller | false        |
| postchange        | This property accepts one string containing a callback function to be called to do any operation after change a record (this is fired on insert and update), this function needs to be defined into current CodeIgniter controller | false        |
| predelete         | This property accepts one string containing a callback function to be called to do any operation before delete a record, this function needs to be defined into current CodeIgniter controller | false        |
| postdelete        | This property accepts one string containing a callback function to be called to do any operation after delete a record, this function needs to be defined into current CodeIgniter controller | false        |

## Field Configuration ##

The fields array configuration is a key based configuration, the key will be the name of field in table, and for each field you can configure:

| **Configuration** | **Description** | **Required** |
|:------------------|:----------------|:-------------|
| type              | The type of field, this property set the field behavior | true         |
| label             | The label of field | true         |
| value             | The default value of field (note: if you were in form edit, this value will be replaced by real value of field in row | false        |
| persist           | This property defines if this field will be persisted in database or not (note: before save data into database, rabbit forms filter the fields to add only valid fields, use this property only if you has a valid field that will not be stored) | false        |
| params            | Associative array that define field parameters (see valid parameters of specific field types) | false        |
| validators        | Validators of field (see more bellow) | false        |

## Validator Configuration ##

Validators can be configured for each field, see base validators configuration:

| **Configuration** | **Description** | **Required** |
|:------------------|:----------------|:-------------|
| type              | Type of validator | true         |
| params            | Parameters of validator (see valid parameters for each specific validator) | false        |

## Retrieve Configuration ##

This configuration defines the behavior of retrieve action:

| **Configuration** | **Description** | **Required** |
|:------------------|:----------------|:-------------|
| manage            | The target controller to manage form data (is important to finish this string with a slash) | controller/method/ |
| remove            | The target controller to delete form data (is important to finish this string with a slash) | controller/removeMethod/ |
| fields            | Array containing fields to display in retrieval | true         |
| view              | This property configures the view of retrieval (the template to display data), read more at view configuration | false        |
| orderby           | This property configure the field to be used to sort data into view | false        |
| pagination        | This property allows you to configure a pagination for data, this attributes accepts one array containing pagination configuration, the required field is only _base\_url_ and _per\_page_, this pagination uses CodeIgniter pagination library and you can use any attributes of this library to configure pagination | false        |
| filters           | You can use this attribute to filter data to be displayed into retrieve view, the value of this field is a numeric array, each element of array is one where expression to be used in the query and the filters will be joined with _and_ operator. | false        |

## View Configuration ##

The view configuration set the behavior of a view:

| **Configuration** | **Description** | **Required** |
|:------------------|:----------------|:-------------|
| template          | Template path of the view | true         |
| params            | Associative array that defines view parameters (see valid parameters for each specific view) | false        |

## Default Configuration ##

Ok, now you know about configuration properties, but you need to know how configuration works.

Rabbit Forms use a default configuration ever, and extends this default with your configuration, if any of your configuration keys conflicts with default configuration, them your configuration will replace the defaults. You can see and change the default configuration at Rabbit Forms configuration file in: application/config/rabbit-forms.php

## And... ##

Ok, that is it, in this page you learned about how Rabbit Forms configuration works and how to use it. See more wiki pages for how to use dynamic configuration or mixed configuration (mixes static configuration and dynamic configuration)