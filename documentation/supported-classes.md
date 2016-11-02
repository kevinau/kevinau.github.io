---
layout: default
title: Supported classes
---
{% include navbar.html parent="documentation" %}

<div id="toc" class="pull-right">
* Documentation
** "Database configuration":databaseConfig
</div>

# {{page.title}}

In order to support data entry, persistence and querying, PennyLedger supports a limited set of Java classes.  The following classes are supported:

* Entity classes.  Classes that represent real world entities.
* Embedded.  Classes that are embedded in other classes.
* References.  Classes that are referenced from within other classes.
* Interfaces.  Place holders for other classes that are determined by entered or runtime values.
* Arrays.
* Lists.
* Sets.
* Maps.  Maps are limited to those with a String key.

Examples will clarify what is supported and what is not.

## Entity classes

Entity classes represent objects that can stand alone in a real life situation.  For example:

* Product.
* Person.
* Invoice.  Maps products sold to a person.

Entity classes are simple Java classes, marked with an @Entity annotation.  They require a unique id and version timestamp.

The following is a very simple entity class:

--- java
@Entity
public class Person {
  @Id
  private int id;
  
  @Version
  private Timestamp version;
 
  @Length(6)
  @Unique
  private String code;
   
  @Length(30)
  private String name;
}
---

## Embedded classes

A class that is embedded within another class.  For example:

> An address class that is made up of, say, street name, town and postal code.  The address class can then be embedded in:
>* Person, as the home address of the person.
>* Invoice, as the delivery address for the goods.

Embedded classes are simple Java classes.  The embedded class can be annotated with @Embeddable, or the reference to 

## References




