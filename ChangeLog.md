## Beta 1.0.5 ##

  * New: Html editor (using TinyMCE)
  * New: File Validator
  * New: Unique Validator
  * Change: Image field auto-add image extensions valitador
  * Change: by default the textfield and textarea doesn't accept html (using htmlentities to reject)
  * Fix: retrieve name at foreign retrieveView
  * Fix: unique validator when editing current row

## Beta 1.0.4 ##

  * New: Image Field
  * New: date can display a value and save another
  * New: list fields accepts orderby and filters at dbsource
  * New: validator base class properties is now exposed
  * New: callback validator
  * Change: redirect is removed from configuration
  * Fix: File field to don't remove files in update (in case of a new file sent)
  * Fix: form doc at getField

## Beta 1.0.3 ##

  * New: orderby at retrieve configuration
  * New: pagination at retrieve configuration
  * New: filters at retrieve configuration
  * New: checkboxgroup field now returns comma separated string with the title values of selected items in displayValue
  * New: form level validation without extending
  * New: form events
  * New: rabbit form configuration extends
  * Change: list field types now return title in displayValue instead of a raw value
  * Fixed: rabbit\_array\_merge behavior
  * Fixed: checkbox field initialization value
  * Fixed: foreign field when no data sent

## Beta 1.0.2 ##

  * New: Foreign Field
  * New: editId propertie into Rabbit\_Form class
  * Change: getShortValue is replaced to getDisplayValue into Rabbit\_Field class
  * Fixed: code doc of factory method into Rabbit\_Form\_Factory class is fixed
  * Fixed: string to get table for retrive is fixed (before it's missing `` and this causes errors when a table uses a reserved name)
  * Refactor: refactor under Rabbit Forms CI Library

## Beta 1.0.1 ##

  * Changed all named "retrive" to "retrieve" (correct spelling)

## Beta 1.0.0 ##

  * First release