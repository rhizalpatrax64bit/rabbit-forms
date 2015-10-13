# DropDown Field #

## Description ##

This field is a select dropdown to allow user to select one item and send data.

This field extends the [List](FieldList.md) field, see [List Field](FieldList.md) description to know how to fill this field data.

## Attributes ##

| **Attribute** | **Description** | **Example** |
|:--------------|:----------------|:------------|
| class         | This attribute defines a class to be added to select html | checkboxClass |
| style         | This attribute defines a inline style to be added to select html | border: 1px solid #aaa; |
| updateField   | This attribute allow you to fill another dropdown data after this field data changes, see details below | see below   |

## Update Field Attribute ##

Is a common need of actually websites to make cascading dropdowns (after you select one option in one dropdown, another dropdown has his data change according to previous dropdown) and Rabbit Forms provides a feature to this.

The _updateField_ attribute accept another array containing update attributes, these are:

| **Attribute** | **Description** | **Example** |
|:--------------|:----------------|:------------|
| target        | The dropdown that will be updated | anotherDropdown |
| url           | The url to request data (this value will be parsed with _site\_url_ method) | controller/action |

The controller page that handles this request will receive a post argument called _value_ that contains the value of source dropdown, and this controller need to echo a JSON markup associative array where keys are the values and values are the titles to put into target dropdown, example:

```
class MyController extends Controller
{
    public function fillDropdown()
    {
        $value = $this->input->post('value');

        $data = array('value' => 'text description', 'value2' => 'another text');

        echo json_encode($data);
    }
}
```

Note the result will need to **only** contains the json data, otherwise will generate javascript errors.