# Form Extends #

By default, Rabbit Forms use a form provider that feature register fields in table, edit fields in table and remove fields from table. In most cases it's all nescessary, but we see longer, and we know the user needs, because of this you can extend form class to provide a high customizable forms, extending form you are able to:

  * change how the data is saved/edited/removed
  * add operations to customize above operations

see details about each item below.

## Change default operations ##

To change how the base operations is madded you can overload these methods:

| **Method** | **Description** |
|:-----------|:----------------|
| saveData   | Overload this method to change how the data is saved |
| editData   | Overload this method to change how the data is edited |
| deleteData | Overload this method to change how the data is removed |

In a basic way you will overload this methods, call the base method and them do some custom operations (like set a date based on date time during save operation), but you can fully rewrite these methods to change how the data is saved (to save data into a xml instead of a database for sample).

example:

```
class Rabbit_Form_User extends Rabbit_Form
{
    public function saveData()
    {
        parent::saveData();
        
        $ci =& get_instance();
        $id = $ci->db->insert_id();

        $ci->db->where($this->getPrimaryKey(), $id)->update($this->table, array('regtime' => date('Y-m-d H:i:s')));
    }
}
```

The example above set the regtime field to actually date just after register item.

note: the editData method and deleteData method receive a first argument containing the id of element that will be edited/deleted