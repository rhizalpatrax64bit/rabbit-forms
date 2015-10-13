# Callback Validation #

## Description ##

This validation is made to create simple custom validators without need to create a validation class.

## Attributes ##

| **Attribute** | **Description** | **Example** |
|:--------------|:----------------|:------------|
| method        | The method to be executed to validate operation, this method needs to be defined in current CI controller | custom\_validate |

The method works like real validator class method, this receives the validator as parameter and you need to return false if it's not ok, or true if it's ok. If it's not ok, you can set the error message by using **setMessage** method of validator.

## Example ##

The following example demonstrate how to validate a time (hours:minutes) using the callback validator.

form.yml
```
fields:
    hour:
        label: Hour
        type: TextBox
        validators:
            -type: Callback
             params:
                method: validate_hour
```

mycontroller.php
```
class MyController
{
    public function validate_hour(Rabbit_Validator $validator)
    {
        $value   = $validator->getField()->getRawValue();
        $matches = array();

        if(preg_match('/(\d{2}):(\d{2})/', $value, $matches)) {
            $hour    = $matches[1];
            $minutes = $matches[2];

            if($hour < 0 || $hour > 23 || $minutes < 0 || $minutes > 59) {
                $validator->setMessage('Invalid time format');
                return false;
            }

            return true;
        } else {
            $validator->setMessage('Invalid time format');
            return false;
        }
    }
}
```