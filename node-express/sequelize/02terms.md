# Sequelize

>Sequelize is a promise-based Node.js ORM ( Object Relational Mapper ) for Postgres, MySQL, MariaDB, SQLite and Microsoft SQL Server. It features solid transaction support, relations, eager and lazy loading, read replication and more.
>
> Official Sequelize Documentation

The library is written entirely in JavaScript and can be used in the Node.JS environment. Sequelize allows us to do many things including:

- [X] Represent models and their data.
- [X] Represent associations between these models.
- [X] Validate data before they gets persisted to the database.
- [X] Perform database operations in an object-oriented fashion.

## ORM (Object Relational Mapper)

An `ORM` \(Object Relational Mapper\) is a piece/layer of software that creates a map between our database into javascript objects that represent our data. This means we can use JavaScript to `create`, `read`, `update`, and `delete` our data instead of writing raw SQL queries.

You can read some more about the benefits of using an ORM [here](http://stackoverflow.com/questions/1279613/what-is-an-orm-and-where-can-i-learn-more-about-it)

**Exercise:** What are 3 pros of an ORM? What are 3 cons?

## Model

A `model` in Sequelize has a name. Usually, models have singular names (such as `User`), while tables have pluralized names (such as `Users`).

A `model` is a javascript object written as a `class` that maps to a data relation \(table\). You can think of a model as the blueprint for what each **row of data** is going to contain. *Each instance of your model represents one row of data*. The ORM allows you perform `CRUD` on instances of your model(s) - which will then be map to the equivalent changes in your database.

## Migration

A `migration` is similar to how we use a version control system such as `Git` to manage changes made to our source code on `Github`, you can use `migrations` to keep track of changes to the database. We are able to transfer changes to our exisiting database schema from one state to anohter. These state transitions are saved in migration files ( ex. `2375934934-create-user.js` ), which describes how to get to the new state and how to revert the changes in order to get back to the old state.

