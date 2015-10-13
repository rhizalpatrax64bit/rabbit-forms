# Field Extends #

Rabbit Forms field extension is one of greatest features of the library, this ables you to create full customized fields as you want.

To create new fields, you first need to understand how the Rabbit Form fields works. You will know about base class Rabbit\_Field that is the base of all Rabbit Fields, any fields that you create needs to extend this class, or extend one that extends it.

## Field name pattern ##

All fields that you create need to be named like: Rabbit\_Field\_FieldName

By default, Rabbit Forms will search for fields into application/rabbit-forms/lib/Rabbit/Field

It's not a good ideia to put your custom fields at this folder because this will mix with default fields and this can cause confusion. You can add more folders to search for fields at rabbit forms configuration file, this configuration is one array and you can add how many folders as you need.

note: the folders added in classpath will not be recusive scaned, and you need to add subfolders if you want to use then.

## Field Composition ##

All Rabbit Forms fields is composed of:

  * one form - this is the form where field is contained
  * one name - the name that represents this field in table
  * one label - the label that describes this field to user (normally a very short string)
  * many attributes - this attributes is madded to able field self customization
  * many validators - these validators will made field to accept only what it needs to accept (note: normally you never add validators at field definition level, but it don't means you can't do it)
  * persist - this simple variable defines if this field will be persisted on database or not (this is normally defined by configuration, but you can change this in definition level too)

Ok, now you know about the fields basics, let's get a little into more.

## Field Methods ##

### Field HTML Generation ###

To make your field works you only need to overwrite one method, this method is **getFieldHtml**.

This method needs to return the HTML code of your field component, it can be simple form fields or full custom javascript controlled fields, depends of your needs.

Remember, in some way, this method needs to refill the field too, so, use **getValue** method to get actually field value and refills the field in appropriated way.

example:

```
class Rabbit_Field_MyField extends Rabbit_Field
{
    public function getFieldHtml()
    {
        $value = $this->getValue();
        $name  = $this->getName();

        return "<input type='text' name='{$name}' value='{$value}' />";
    }
}
```

### Field Attributes ###

The field attributes is initialized by configuration loader, you can simple use the  object variable **$attributes** but it is discourage because you can get some errors when try to get an index that is not defined.

To help you, the base field class provides a method called **getAttribute** that checks if attribute is set before retrieve it, and if the index is not set, it return nulls. You can pass a second argument to this method indicating a default value to be returned instead of null.

example:

```
class Rabbit_Field_MyField extends Rabbit_Field
{
    public function getFieldHtml()
    {
        $value = $this->getValue();
        $name  = $this->getName();
        $style = $this->getAttribute('style', '');

        return "<input type='text' name='{$name}' value='{$value}' style='{$style}' />";
    }
}
```

### Field Parsing Data ###

Sometimes the data of field do not come exactly in the way that field needs to be saved into database, in this cases you need to parse the data to make database correct string, and after you need to reconvert to inputed form.

To perform this operation you can overwrite the methods **getValue** and **setValue** of field.

One example of this behavior is when you receive a checkbox group, the value passed in post data to checkbox is one PHP array and not a string, in this case the function **serialize** of PHP is used to make a db-save version of data and **unserialize** to retrieve original data.

example:

```
class Rabbit_Field_MyField extends Rabbit_Field
{
    public function getValue()
    {
        return unserialize($this->value);
    }

    public function setValue($value)
    {
        $this->value = serialize($value);
    }
}
```

note: the field base class has two methods called **getRawValue** and **setRawValue**, this methods return the db-version string of field, this methods is declared as final and cannot be replaced.

### Field Assets ###

Sometimes your fields will need some external assets (like css or javascript codes), for this propose the form class provide an assets manager, this is a simple assets controller and when fields defines required controllers this manager ensures that no more than one copy of each resource is used. To add one asset to manager you will use the method **addAsset** of form class.

example:

```
class Rabbit_Field_MyField extends Rabbit_Field
{
    public function initialize()
    {
        $this->form->addAsset('jquery-1.2.3.pack.js');
    }
}
```

The method **initialize** (the method overloaded in example above) is called after the field is ready (with attributes, validators and etc), so you can use these things to initialize the assets.

note: the base path of assets is the Rabbit Forms assets folder, this path can be configured in Rabbit Forms configuration file.

### Field Inline Execution ###

In addiction to field assets (that was loaded before the form content), there are field inline execution too, with this feature you can add javascript code to run after code html content (this way the form components is available). This is very useful to run code into fields of form, like apply the mask to input, or start your component after her html is loaded.

example:

```
class Rabbit_Field_MyField extends Rabbit_Field
{
    public function initialize()
    {
        $this->form->addClientExec('alert("The form is loaded")');
    }
}
```

## Summary ##

This page described how the field component works and all the needs to create a new one. To see real uses of this, check out into Rabbit Forms basic Field Components at source code.