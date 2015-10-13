# Validation Extends #

Rabbit Forms provides a simple way to create your own field validators.

The basics to extend a validator is simple, you only need to overwrite one method, see above.

## Validator name pattern ##

All validators that you create need to be named like: Rabbit\_Validator\_ValidatorName

By default, Rabbit Forms will search for validators into application/rabbit-forms/lib/Rabbit/Validator

It's not a good ideia to put your custom validators at this folder because this will mix with default validators and this can cause confusion. You can add more folders to search for validators at rabbit forms configuration file, this configuration is one array and you can add how many folders as you need.

note: the folders added in classpath will not be recusive scaned, and you need to add subfolders if you want to use then.

## Validate Method ##

The **validate** is the method that you will extend to implement your validator. When implementing this method you need to do your validation and return true if the test pass or false otherwise.

If your validation fails, you need to change message value of validator before return false, this message will be passed to layout at and, showing error message to user.

example:

```
class Rabbit_Validator_GreaterThanTen extends Rabbit_Validator
{
    public function validate()
    {
        $value = $this->field->getRawValue();

        if($value <= 10) {
            $this->message = 'The field is lesser or equals a ten';
            return false;
        }

        return false;
    }
}
```

This is a simple sample, above you will read about validator provided features to help you with field validation.

## Valitador Composition ##

The validator base class is composed of:

  * one field - field that will be validated
  * many parameters - parameters to set validator settings
  * message - the error message to display

## Validator Parameters ##

The validator parameters is passed by configuration and can be used to customize validators, the parameters is saved into _$params_ variable, but the validator provides the method **getParam(string $name, mixed $default = null)** to help you when getting these parameters

## Summary ##

This page describes how to create your own validators, we know the real cases is more complex than things describled here. Check base validators to code to see the how the real validators is madded.