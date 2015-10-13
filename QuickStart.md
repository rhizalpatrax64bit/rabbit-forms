# Warning: this page is outdated and will be changed, please dis consider this page until this warning is removed. #

# Quick Start #

Let's build a form with Rabbit Forms!

First you need to install Rabbit Forms, if it's not installed see [installing wiki page](Installing.md).

The process to create a form is very simple, you only need to has a table into database, create a configuration file and then use Rabbit Forms to display this data, let's create a sample form:

users.yml
```
table: user
primary_key: user_id
fields:
    name:
        type: TextBox
        label: User Name
        validators:
            - type: Required
    email:
        type: TextBox
        label: E-Mail
        validators:
            - type: Email
    login:
        type: TextBox
        label: Login
        validators:
            - type: Required
    password:
        type: TextBox
        label: Password
        params:
            mode: password
        validators:
            - type: Required
            - type: Length
              params:
                  min: 3
    passconfirm:
        type: TextBox
        label: Confirm Password
        persist: false
        params:
            mode: password
        validators:
            - type: Required
            - type: Compare
              params:
                  compareTo: password
retrieve:
    fields:
        -name
        -login
        -email
redirect: 'rabbitcontrol/retrieve/users'
```

The table creation:
```
create table user (
    user_id bigint(10) not null auto_increment,
    name varchar(200),
    login varchar(80),
    email varchar(255),
    password varchar(180),
    primary key(user_id)
)
```

Ok, it can be scary at first, but is really simple. This is a complete form, with validations in all fields, this is a quick start, for bigger explanations in wiki for more content.

Save this file with name users.yml in folder "application/rabbit-forms/forms", you can use the name you want, the name of file don't matter, and if you want, you can manage classpath of forms folders at rabbit-forms configuration file.

Next step, after the file is saved you can use this by Rabbit Controller, simple access the url:

http://yoursite.com/rabbitcontroller/retrieve/users

Oh yeah, you will take to a ugly page with a link to add a new record, and a table displaying saved records, you can test this at time. The layout of this controller will be improved in next versions ;)

And at is guys, this is a simple quickstart to see anything working, please read the other wiki pages to see how to make wounder full things like:

  * [understanding the configuration file](Configuration.md)
  * [customize layout](Templating.md)
  * [all featured fields](Fields.md)
  * [all featured validators](Validations.md)
  * [extending fields](FieldExtend.md)
  * [extending validators](ValidationExtend.md)

and much more ;)