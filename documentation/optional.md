---
layout: default
title: Optional field annotation
---
{% include navbar.html parent="documentation" %}

# {{page.title}}

An indication that the annotated field can accept spaces for data entry.  If the data entry field is empty, the annotated field will be assigned a `null` value.

"Blank" means that the data entry field appears to have no entered characters.  That is, no characters have been entered, or the entered characters are only spaces.

A blank field is not the same as a field with a default showing.  If a field has a default value, that value will be displayed prior to any data entry.  In this case, if the form is accepted, the field will be assigned the default value.  On the other hand, if one or more spaces are entered (so the default value is removed) the data entry field will be blank.  In this case, if the form is accepted, the field will be assigned a `null` value.

|Annotation|Effect|
|-
|@Optional or @Optional(true)|The annotated field can accept an blank data entry.  If the data entry is blank, the annotated field will be assigned a `null` value.|
|@Optional(false)|The annotated field cannot accept just spaces for data entry.|

## String based types

If a String data entry field is entered as blanks:

* If it is `Optional`, the String field will be assigned a `null` value.
* If it is `Optional(false)`, the String field will be assigned a zero length string[^1].

[^1]: Leading and trailing spaces are removed from all data entry fields.

The same is true of all String based types (provided the type validation rules are adhered to).

## Examples

{% highlight java %}
public class DataEntryForm {

  private int field1 = 123;
  
  @Optional
  private Integer field2 = 234;
  
  @Optional(false)
  private Integer field3 = 345;
  
}
{% endhighlight %}

`field1` is a primitive type, and so cannot be `Optional`.  `field1` has a default value of 123 and this will display as "123".  If this data entry field is blanked out, an error will be reported "Not a valid integer value".

`field2` is marked as `Optional`.  `field2` has a default value of 234 and this will display as "234".  If this data entry field is blanked out, the field value will be assigned a `null` value.

`field3` is marked as `Optional(false)`.  `field3` has a default value of 345 and this will display as "345".  If this data entry field is blanked out, an error will be reported "Not a valid integer value".  It is not optional.  A value must be entered or accepted as a default value.

