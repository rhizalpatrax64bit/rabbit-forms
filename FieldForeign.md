# Foreign Field #

## Description ##

This field provides a check table to make relations between tables using foreign key fields, actually this field supports one to many and many to many relations (if you want many to one relation you can to by simple using [DropDown](FieldDropDown.md) field).

## One to many relations ##

One to many relations occur when a table has a foreign key field to another table into a row data. Check the sample:

table user
```
id bigint(10)
name varchar(255)
email varchar(255)
```

table task
```
id bigint(10)
task text
user_id bigint(10)
```

The above sample show a situation when a task has a foreign key to user field, it means, one user can has **many** tasks, but one task is related only to **one** user, this is a **one to many** relation (one user, many tasks).

Let's check now, you has a user manage form, and want to be able to select tasks to associate with user into user manage form, let's do this!.

At first, lets create a configuration file for manage tasks:

task.yml
```
table: task
primary_key: id
fields:
  task:
    type: TextArea
    label: Task
retrieve:
  manage: task/manage/
  delete: task/delete/
  fields:
    -task
```

Ok, with above code you can manage the tasks, now let's get into user form

user.yml
```
table: user
primary_key: id
fields:
  name:
    type: TextBox
    label: Name
  email:
    type: TextBox
    label: E-Mail
  tasks:
    type: Foreign
    label: Tasks
    params:
      config: task.yml
      type: onemany
      foreign: user_id
retrieve:
  manage: user/manage/
  delete: user/delete/
  fields:
    -name
    -email
```

It's all :)

The key name of field a foreign field doesn't matter, use the key as you mean better, let's check the foreign field params when use one-to-many relation:

| **Attribute** | **Description** | **Example** |
|:--------------|:----------------|:------------|
| config        | This is the configuration of foreign table, this attribute accepts the YAML path of configuration or a inline array configuration (using yml array format) | foreign.yml |
| type          | This is the type of relation, actually supports "onemany" and "manymany" | onemany     |
| foreign       | The foreign field name, this is the name of foreign key id of this table into another table | this\_foreign\_id |

## Many to many relations ##

Now let's upgrade above example, now the tasks of system need to be assigned to more than one user, this means one user can has many tasks and a task can be assigned to many users, this figures a **many to many** relation.

The database need to be upgrated, to make a many to many relation we need a third table to make associations, first remove the foreign field from tasks table and create a relational table:

table users\_tasks
```
id bigint(10)
user_id bigint(10)
task_id bigint(10)
```

tip: for relational fields and tables, make sure to index every foreign field, this will improves the database performance. In example above the id is a primary key index, and you need to create one index to user\_id field and one index to task\_id field.

The relational table is madded, now let's update user form configuration:

user.yml
```
table: user
primary_key: id
fields:
  name:
    type: TextBox
    label: Name
  email:
    type: TextBox
    label: E-Mail
  tasks:
    type: Foreign
    label: Tasks
    params:
      config: task.yml
      type: manymany
      table: users_tasks
      local: user_id
      foreign: task_id
retrieve:
  manage: user/manage/
  delete: user/delete/
  fields:
    -name
    -email
```

And this is all we need, only the tasks field is changed, let's see **many-to-many** relation attributes:

| **Attribute** | **Description** | **Example** |
|:--------------|:----------------|:------------|
| config        | This is the configuration of foreign table, this attribute accepts the YAML path of configuration or a inline array configuration (using yml array format) | foreign.yml |
| type          | This is the type of relation, actually supports "onemany" and "manymany" | onemany     |
| table         | The table that makes relations between fields | relational\_table |
| local         | The field that contains local table id | local\_id   |
| foreign       | The field that contains foreign table id | foreign\_id |

And that is all, the relations is madded :)

## Foreign table templating ##

The table displayed by foreign field can be templated, the view base code is differente from base retrieve because this table needs the checkboxes elements, the templating is very look like retrieve templaing.

For base templating, the table contains the same class styles of retrieve element, but it's add specific classes to foreign table, this way the table gets the style templaing of retrieve view, but you can extend the template to specific foreign table view.

The base table code is displayed below:

```
<div class="rabbit-retrive-foreign-container">
    <table class="rabbit-retrieve-table rabbit-retrieve-table-foreign" cellspacing="<?= $params->get('tableSpacing', '2') ?>" cellpadding="0">
        <thead>
            <tr>
                <td></td>
                <?php foreach($fields as $field): ?>
                <td><?= $field ?></td>
                <?php endforeach; ?>
            </tr>
        </thead>
        <tbody>
            <?php foreach($rows as $row): ?>
            <tr>
                <td><?= $row['rabbit_foreign_check'] ?></td>
                <?php foreach($kfields as $field): ?>
                <td><?= $row[$field] ?></td>
                <?php endforeach; ?>
            </tr>
            <?php endforeach; ?>
        </tbody>
    </table>
</div>
```

How you see, another diference is the div containing the table, this div is created for main porpuse to create scroll if you want.

If you want, you can create your own template, to do this add the parameter **retrieveView** containg the path of view.

The templating follow the same Rabbit Forms templating way, see [Templating](Templating.md) documentation to more information.