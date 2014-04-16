PeeweeMySQLObjects
==================

A (soon-to-be) full-featured MySQL database introspection tool to reverse-engineer MySQL databases into Python objects.
Uses Peewee from Coleifer (get it from https://github.com/coleifer/peewee or http://peewee.readthedocs.org/en/latest/)

Even though Pwiz exists, I coded this before knowing about it. I proceeded to add support for ENUM, foreign keys and unique indexes.

COMPATIBILITY
* Not compatible with PostgreSQL or SQLite ! MySQL only.
* Works best with the InnoDB engine. Works with the MyISAM engine.
* Compatible with Windows, Linux and Mac. 

USAGE
* $ peeweemysqlobject userlogin passwd databaseName

RESTRICTION
* Logged user must be able to read from the information_schema database.
* Logged user must have the PROCESS privilege to query the INNODB_SYS_FOREIGN table, if applicable.

TODO
* Add support for remote databases. For now, only local databases are supported.
* Reorder column definitions in generated files. They are stored and sorted in a dict, so they come out in another order than what's given by the ordinal_position.
* Send your ideas at broutta.mickael(at)gmail.com !

WHAT'S DONE
* The FOREIGN KEY "_id" issue has been fixes. [v 0.1.0.5]
* Support for indexes (non-uniques and uniques, for all columns, even if they are part of multiple indexes) [v. 0.1.1.1]
* better naming system for "related_name"s
    * related_names will now have an underscore followed by a number appended starting with the second occurence of a foreign key on the same foreign table (eg. "fk_reftable_refcol_num").
* clean-up of global variables (dbname, login, passwd). They can't be used when importing parts of the module like "from peeweemysqlobjects import get_tables"
    * Clean-up done, no more glaring global.
* on_update and on_delete actions for foreign keys

KNOWN ISSUES & TROUBLESHOOTING
* More related to peewee. Any Foreign key will have a "_id" appended. It can create situations like this one : your table has a Foreign key column named tablename_Id, 
    and peewee appends "_id". MySQL will report that "tablename_Id_id" doesn't exist, which is true. I need to either think about a workaround, or ask Coleifer why he
    made peewee append "_id". There must be a reason.
    SOLUTION : A fix is being worked on and needs testing.
