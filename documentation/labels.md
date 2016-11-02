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

In addition, the labels can be specified in different places:

* In form templates
* In Java code annotations
* Derived from Java code

These are also described below.

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
  being asked for, the hint may be "mm/yy".
  
  In web forms, the hint is displayed as part of the <label> element, but in a smaller font than the label.
  
Description
: A piece of text that describes the data entry field.  In web forms, the description is displayed as a paragraph following the data
  entry field.  The description should not repeat the label--it should contribute additional information about the data entry field--and
  it should only be used when necessary.  The the purpose of the data entry field is obvious, no description should be provided.
