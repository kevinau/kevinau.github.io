---
layout: default
title: Database
---
{% include navbar.html parent="configuration" %}

<div id="toc" class="pull-right">
* Configuration
** "Database configuration":databaseConfig
</div>

# {{page.title}}

PennyLedger requires a database to work.  By default, it uses a built-in database, but you can configure it to use a select number of different databases.

PennyLedger has been tested using the following databases:

* Derby embedded.  This is the default database.  The database is stored on the file system under the user's home directory.  This database is single user only--it can only be used by one user at a time.

* Derby server.  This is a multi-user version of the Derby database.  Once the Derver server databases has been started, multiple PennyLedger users can connect to it and share the data.

* Postgresql.  This is a multi-user database server.

The following databases will be supported if there is demand, and if time and resources exist:

* DB2.
* MySQL.
* Firebird.
* Microsoft SQL server.
* Oracle.

## Database configuration

In the configuration directory of PennyLedger, create a file called

`org.pennyledger.db.Database-xxx.cfg`

where xxx is replaced with a short name you want to give this database.  For example, if you are creating a database for your home accounts, you could call it "home".  The configuration file will then be:

`org.pennyledger.db.Database-home.cfg`

This file should be laid out as a Java "properties" file.  It should contain the following:

```
name = xxx
dialect = ddd
server = sss
dbname = ttt
username = nnn
password = ppp
```

where:
* `xxx` is your name for this database.  This should be the same ss the last part of the configuration file name.
* `ddd` is the type of database.  It can be one of: derbyEmbedded, derbyServer, postgresql, db2, mysql, sqlServer, firebird, or oracle.  Other database types can be added as OSGi components.
* `sss` is the name of the server where the database is running.  The sss must conform to the requirements of the database type.  For example, if the dialect is derbyEmbedded, sss will name a filename on the local file system.  If the dialect names one of the other databases, sss will be a domain name, with an optional post number.
* `ttt` is the name of the database on the server.
* `nnn` is the user name as required by the databases.
* `ppp` is the user password as required by the database.

The following is an example database configuration file:

```
name = home
dialect = postgresql
server = localhost:1234
dbname = pennyledger
username = kevin
password = 123456
```

When this file is created, a database connection will be made to the specified database.  The success (or otherwise) of this connection will be logged by PennyLedger:

* If there is no log entry--success or fail--check the following:
** Was the file created in the right directory.  The configuration directory should be on the server that is running PennyLedger.  It should contain the configuration file:

`org.pennyledger.about.ConfiguratedAbout.cfg`

** Is the name of the configuration file correct.  It must be:

`org.pennyledger.db.Database-xxx.cfg` where xxx is your name for this database.

The last part of the file name (the xxx) does not matter, but the `org.pennyledger.db.Database` and the `.cfg` does.

* If the the log entry reports an error, the error message should explain the problem.  You shuold be able to edit the configuration file and save it.  When the file is saved, a database connection will be attempted again.

* If the log entryPennyLedger will read it again and attem
Whether an data entry field allows data entry, is view only, or is not applicable to the form.

There is an enumeration "EntryMode" that is used for data entry mode:

* EntryMode.ENTRY := Normal data entry is allowed.
* EntryMode.VIEW := The value of the data entry field is displayed but no changes can be made.
* EntryMode.NA := The data entry field is not applicable in this form.  For example, if a form has a checkbox for "isTaxApplicable", a tax rate field would be not applicable if this checkbox was clear.

If an entry field is not applicable, the field and field label are not shown--they occupy no space of the form.
^

## Example

```
public class DataEntryForm {

  @FormField(mode=EntryMode.ENTRY, length=5)
  private String locationCode;
  
  @FormField(mode=EntryMode.VIEW)
  private String locationName;
  
  private boolean difficultDelivery;
  
  private double deliveryCost;
  
  // ... other logic
  
  @ModeFor("deliveryCost")
  private EntryMode deliveryCostMode () {
    if (difficultDelivery) {
      return EntryMode.ENTRY;
    } else {
      return EntryMode.NA;
    }
  }
  
}
```

`locationCode` is a conventional data entry field.  In this example it is 5 characters in length.

`locationName` is a conventional view or display field.  It is assumed there is some logic (not shown) that retrieves the location name when a location code is entered.

`deliveryCostMode` is a method that returns the entry mode for `deliveryCost`.  If `difficultDelivery` is entered as true (the boolean checkbox is checked), the entry mode for `deliveryCost` will be `EntryMode.ENTRY`.  That is, `deliveryCost` will be a conventional data entry field.  If, however, `difficultDelivery` is entered as false (the boolean checkbox is clear), the entr mode for `deliveryCost` will be `EntryMode.NA`.  In tis case, `deliveryCost` (and its associated label) will not be shown at all.
