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
$ peeweemysqlobject userlogin passwd databaseName

RESTRICTION
Logged user must be able to read from the information_schema database.

TODO
* SOLVE THE FOREIGN KEY "_id" ISSUE (created by https://github.com/coleifer/peewee/blob/master/peewee.py line 895) [TO BE TESTED]
* on_update and on_delete actions for foreign keys
* better naming system for "related_name"s [DONE]
* clean-up of global variables (dbname, login, passwd). They can't be used when importing parts of the module like "from peeweemysqlobjects import get_tables" [TO BE TESTED]
* and some more...

KNOWN ISSUES & TROUBLESHOOTING
* More related to peewee. Any Foreign key will have a "_id" appended. It can create situations like this one : your table has a Foreign key column named tablename_Id, 
    and peewee appends "_id". MySQL will report that "tablename_Id_id" doesn't exist, which is true. I need to either think about a workaround, or ask Coleifer why he
    made peewee append "_id". There must be a reason.
    SOLUTION : A fix is being worked on and needs testing.
