---
layout: default
title: Optional field annotation
---
{% include navbar.html parent="documentation" %}

# @{{page.title}}

An indication that the annotated field can accept spaces for data entry.  If the data entry field is empty, the annotated field will be assigned a `null` value.

"Blank" means that the data entry field appears to have no entered characters.  That is, no characters have been entered, or the entered characters are only spaces.

A blank data entry field is not the same as a data entry field with a default showing.  If a field has a default value, that value will be displayed prior to any data entry.  In this case, if the form is accepted, the field will be assigned the default value.  On the other hand, if one or more spaces are entered (so the default value is removed) the data entry field will be blank.  In this case, if the form is accepted, the field will be assigned a `null` value.

Fields that are Java primitive types cannot be assigned a `null` value.  The `@Optional` annotation cannot be used on fields that are Java primitive types.

## Example

{% highlight java %}
public class DataEntryForm {

  private int field1 = 123;
  
  @Optional
  private Integer field2 = 234;
  
  @Optional(false)
  private Integer field3 = 345;
  
}
{% endhighlight %}

`field1` is a primitive type, and so cannot be `@Optional`.  `field1` has a default value of 123 and this will display as "123".  If this data entry field is blanked out, an error will be reported "Not a valid integer value".

`field2` is marked as `@Optional`.  `field2` has a default value of 234 and this will display as "234".  If this data entry field is blanked out, the field value will be assigned a `null` value.

`field3` is marked as `@Optional(false)`.  `field3` has a default value of 345 and this will display as "345".  If this data entry field is blanked out, an error will be reported "Not a valid integer value".  It is not optional.  A value must be entered or accepted as a default value.

## String based types

If a String data entry field is entered as blanks:

* If it is `@Optional`, the String field will be assigned a `null` value.
* If it is `@Optional(false)`, the String field will be assigned a zero length string (leading and trailing spaces are removed from all data entry fields).

The same is true of all String based types.

## Boolean type

The Boolean type is an exception to the rule about entering blank values.  Boolean type fields are represented as checkboxes, with the following values:

* Checked [x].  The field is assigned a `Boolean.TRUE` value.
* Unchecked [ ].  The field is assigned a `Boolean.FALSE` value.
* Blank [-].  The field is assigned a `null` value.

The problem with the Boolean type is that it uses the checked/unchecked representation that is typical of boolean types, leaving a "blank" representation that is not blank!

In addition, the space bar is used to toggle between the checked/unchecked/blank representations.  The space bar does not "blank out" the Boolean representation like it does for other types.

If `@Optional` is specified for a Boolean type, the data entry field is represented using the three checkbox states described above.  If `@Optional(false)` is specified, the data entry field is represented using the three checkbox states descibed above, but if blank is selected, an error message is displayed "... must be checked or unchecked".

