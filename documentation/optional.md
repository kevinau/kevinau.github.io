---
layout: default
title: Optional field annotation
---

<!--
{% include navbar.html parent="documentation" %}
-->

@{{page.title}}
===============

The `@Optional` annotation indicates that a field can be `null`.

If a field is annotated with `@Optional` or `@Optional(true)`, the field can be `null`.  If the field has no `@Optional` annotation, 
or is annotated with `@Optional(false)`, the data entry field cannot be `null`.

is blank, the field value will be `null`.

`@Optional(false)`
: The field cannot be `null`.  If the data entry field is blank:
  * If a zero length String is an acceptable value (such as in String data types), the value will be a zero length String.
  * Otherwise an error will be reported.

In the above, "blank" means that the data entry field appears to have no entered characters.  That is, no characters have been entered,
or the entered characters are only spaces.  A "blank" field is also described as being "empty".

A blank data entry field is not the same as a field with a default value showing.  If a field has a default value, 
that value will be displayed prior to any data entry.  If the form is then accepted, the field will be assigned 
the default value.  On the other hand, if one or more spaces are entered (so the default value is removed) the data entry 
field will be "blank" and subject to any `@Optional` annotation. 

The `@Optional` annotation is similar to the `org.eclipse.jdt.annotation.Nullable` annotation.  The Eclipse `Nullable` 
annotation cannot be used because is retention is `CLASS` and is not available at runtime.

Primitive types
---------------

Fields that are Java primitive types cannot be assigned a `null` value, do it does not make sense to annotate such fields
with the `@Optional` annotation.

String based types
------------------

If a String data entry field is entered as blanks:

* If it is `@Optional`, the String field will be assigned a `null` value.
* If it is `@Optional(false)`, the String field will be assigned a zero length string (leading and trailing spaces are
removed from all data entry fields).  

The same is true of all String based types.

Numeric types
-------------

Numeric types provide a good example of how to use `@Optional`.  The following example shows the 

~~~ java
public class DataEntryForm {
  
  private int field1 = 123;
   
  @Optional
  private Integer field2 = 234;
  
  @Optional(false)
  private Integer field3 = 345;
    
}
~~~

`field1` is a primitive type, and so cannot be `@Optional`.  It has a default value of 123 and this will display
as "123".  If this data entry field is blanked out, an error will be reported "Not a valid integer value".

`field2` is marked as `@Optional`.  It has a default value of 234 and this will display as "234".  If this data
entry field is blanked out, the field value will be assigned a `null` value.

`field3` is marked as `@Optional(false)`.  It has a default value of 345 and this will display as "345".  If
this data entry field is blanked out, an error will be reported "Not a valid integer value".


Boolean type
------------

While the rules for Boolean type fields are the same as for all other fields, Boolean data entry fields 
are handled differently.

Boolean type fields are represented as checkboxes that typically looks like:

![](/images/tri-state-checkbox.png)

If a Boolean field has no `@Optional` annotation, or is annotated with `@Optional(false)`, the data entry field will
allow two values: checked and unchecked:

* If checked, the field is assigned a `Boolean.TRUE` value.
* If unchecked, the field is assigned a `Boolean.FALSE` value.

If the Boolean field is annotated with `@Optional` or `@Optional(true)` the data entry field will allow three values:
checked, unchecked and indeterminate.

* If checked, the field is assigned a `Boolean.TRUE` values.
* If unchecked, the field is assigned a `Boolean.FALSE` value.
* If indeterminate, field is assigned a `null` value.  This is equivalent to a blank data entry field.

It would be nice to use three values such as: [&#x2713;] for true, [&#x2715;] for false, and blank for 
null.  Unfortunately, the checked and unchecked, for true and false, is too widely established to change.

In addition, for checkboxes, the space bar is used to toggle between the checked/unchecked/blank representations.
The space bar does not blank out the Boolean representation like it does for other types.

