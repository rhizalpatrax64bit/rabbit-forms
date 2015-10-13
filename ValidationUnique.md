# Unique Validation #

## Description ##

This is a simple validator to rejects repeated entries in the table, this validator will search for the input value in fields of same table and will give a error if the inputed value is found.

## Example ##

This example demonstrate how to use Unique Validator to reject repeat logins into a system.

```
fields:
    login:
        label: Login
        type: TextBox
        validators:
            -type: Unique
```