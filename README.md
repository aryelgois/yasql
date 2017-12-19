# Intro

**YAML Ain't SQL** is a [YAML] specification to define SQL database schemas.

It aims to make easier to write and maintain simple database schemas in a human
friendly format.


# Specification

A YASQL file is a ordinary `.yaml` with a single document containing the
following keys:

> Other keys are implementation defined


## database

Contains a map of data about the database. The only required key is `name`.

Possible keys:

- name: the database name
- charset: the database character set (default: `UTF8`)
- collate: the database collation (default: `utf8_general_ci`)
- source: the SQL implementation to adhere (default: `MySQL`)


## tables

A map of tables and their columns. Each column specifies its type and some other
settings (e.g. PRIMARY KEY or AUTO_INCREMENT) in a plain string.

Some notes:

- All columns are implicitly NOT NULL. To define a nullable column, add a `NULL`
  or `NULLABLE` keyword.

- All numeric columns are implicitly UNSIGNED. To define a signed column, add a
  `+` before or after the column type: `cash: +int` or `rating: tinyint(1)+`

- A shortener for the `FOREIGN KEY` keyword is `->`


## composite

A list of strings defining Multiple-Column Indexes. The format is:

`KEYWORD table column1 column2 ...`

With this, it's possible to define a composite of PRIMARY KEY or UNIQUE indexes,
for example.


## definitions

A map of custom column definitions which can be reused.

If the first word of a column value is a `definitions` key, it is replaced by
the corresponding value. Definitions can extend other definitions.

> Be aware of circular reference.  
> With great recursion power comes great responsibility.


[YAML]: http://yaml.org/
