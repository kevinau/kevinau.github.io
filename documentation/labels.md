---
layout: default
title: UI labels
---

<!--
{% include navbar.html parent="documentation" %}
-->

UI labels
=========

Data entry fields on a form are surrounded by labels.  These labels inform the user what data entry is required to complete the form.

Each different data entry field has a different set of labels.  For example:

* Entities have titles, short titles and descriptions.
* Simple fields have labels, hints and descriptions.
* Embedded fields have headings and descriptions.
* Arrays and lists have headings and descriptions.  They also have labels for each entry within the array or list.
* References to entities
* Interfaces

In addition, the labels can be specified in different places:

* Derived from Java code
* Java code annotations
* Form templates

These are described below.

Different sets of labels
========================

Entities
--------

Entities (classes annotated with @Entity) have the following labels:

Title
: A short piece of text that describes the entity.  Where an entity is being viewed or edited using a web form, the title is displayed at the 
  top of the page as a <h1> element.
  
Short title
: A very short piece of text that is an abbreviation of the title.  This text will describe the entity, but is shorter in length than the
  title.  It is used in menus and browser tabs.  
  In web forms, the short title will be used in the <title> element.
  
Description
: A piece of text that describes the entity.  In web forms, the description is displayed as a paragraph following the <h1> element.
  The description should not repeat the title--it should contribute additional information about the entity.

Simple data entry fields
------------------------

Simple data entry fields can have the following labels:

Label
: A short piece of text that describes the field.  It identifies to the user what the data entry field is about.  Examples are:
  
  * User name
  * Town or suburb
  * Date of birth
  * Gender
  
  In web forms, the label is included in a <label> element that references the data entry field.
  
Hint
: A very short piece of text that gives a hint as to the format of the data entry expected.  For example, if a payment card expiry date is 
  being asked for, the hint may be "mm/yy".  Hints should only be specified if the format of the data entry is not obvious.
  
  In web forms, the hint is displayed as part of the <label> element, but in a smaller font than the label.
  
Description
: A piece of text that describes the data entry field.  In web forms, the description is displayed as a paragraph following the data
  entry field.  The description should not repeat the label--it should contribute additional information about the data entry field--and
  it should only be used when necessary.  If the purpose of the data entry field is obvious, no description should be provided.

Embedded fields
---------------

Embedded fields (using the @Embedded tag, or referencing a class annotated with @Embeddable) can have the following labels:

Heading
: A short piece of text that introduces the group of fields that make up the embedded field.  For example, if you are embedding two 
  address fields, you might label one "Delivery address" and the other "Postal address".
  
  In web forms, the heading is displayed as a <legend> within a <fieldset>.
  
  An embedded field heading can be omitted if the intention of the embedded fields is obvious.
  
Description
: A piece of text that describes the embedded fields.  In web forms, the description is displayed as a paragraph following the <legend> 
  within the <fieldset>.  The description should not repeat the heading--it should contribute additional information about the embedded 
  fields--and it should only be used when necessary.  If the purpose of the embedded fields is obvious, no description should be provided.

Arrays and lists
----------------

Arrays and lists can have the following labels:

Label
: A short piece of text that describes the array or list.  This is used like the label on simple data entry fields described above.

Hint
: A very short piece of text that describes how many elements the array or list can have.  This is used like the hint on simple data entry
  fields described above.
  
A description label is not used on arrays or lists[^1].

[^1]: Should a decription label be allowed on arrays and lists?

Index labels
: A set of labels that name each element of an array or list.  Typically this wil be integers starting at 1: 1, 2, 3, 4, etc; but it can be
  something more complicated.  For example, if the array is an array of months, the element labels should be the the names of the month.
  
References to entities
----------------------

References to interfaces are labeled the same way as simple data entry fields.

Interfaces
----------

Not yet decided.

Specifying labels
=================

Derived from Java code
----------------------

Labels do not have to be specified as they can reasonably be derived from Java code.

Consider the following entity class:

~~~ java
@Entity
public class ClubMember {

  private String name;
  
  private LocalDate dateJoined;
  
}
~~~

The title and short title for the entity is "Club member".  This is derived from the class name by interpreting the camel case class name.

The field labels are "Name" and "Date joined".  These are derived from the field names by interpreting the camel case field names.  There are no hint or description labels.

If you name your classes and fields well, you can rely on the default labels for most web forms.

Java code annotations
---------------------

Sometimes the class or field names do not lend themselves to interpretation.  For example, you may have a field name "townSuburb", but want a
label of "Town or suburb".  You can achieve this by adding a @Label annotation.  For example, within an entity class:

~~~ java
@Label("Town or suburb")
private String townSuburb;
~~~


