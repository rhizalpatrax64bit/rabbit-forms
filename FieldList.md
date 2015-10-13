# List Field #

## Description ##

This field is a abstract field (you can't use this in field type configuration) that provides common data manager to list field types, the actually fields that is list type base is:

  * [CheckBoxGroup](FieldCheckBoxGroup.md)
  * [DropDown](FieldDropDown.md)
  * [RadioGroup](FieldRadioGroup.md)

Any of these fields support List field attributes described below.

## Attributes ##

| **Attribute** | **Description** | **Example** |
|:--------------|:----------------|:------------|
| items         | This attribute is one associative array that contains data of field items (the key is the value and the title is the value | see below   |
| dbsource      | This attribute defines a database source to get data and fill field | see below   |

## Items Attribute ##

Items attribute is very simple, follow the example below:

```
fields:
    civil_state:
        type: DropDown
        label: Civil State
        params:
            items:
                single: Single
                married: Married
                divorced: Divorced
                widowed: Widowed    
```

## Database Source Attribute ##

The database source is a powerfully attribute that get a data from one database table and fills the list field, the attributes of database source is described below:

| **Attribute** | **Description** | **Example** |
|:--------------|:----------------|:------------|
| table         | The table where the data is requested | countries   |
| title         | The field in table where script keep the item title | country\_name |
| value         | The field in table where script keep the item value | country\_id |
| orderby       | Optional field to set's data sorting | country\_name asc |
| filters       | Optional filters to restrict data | _see below_ |

Example:

```
fields:
    user_nationalities:
        type: DropDown
        label: User Nationalities
        params:
            dbsource:
                table: countries
                title: country_name
                value: country_id
                orderby: country_name asc
                filters:
                    -active = 1
```

ps: the _asc_ can be omitted