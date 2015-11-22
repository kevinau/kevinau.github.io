---
layout: default
title: Optional field annotation
---
{% include navbar.html parent="documentation" %}

An indication that the annotated field can accept an empty (or blank) data entry field.  If the data entry field is empty, the annotated field will be assigned a `null` value.

"Blank" means that the data entry field appears to have no entered characters.  That is, no characters have been entered, or the entered characters are only spaces.

A blank field is not the same as a field with a default showing.  If a field has a default value, that value will be displayed prior to any data entry.  If the form is accepted with a default field value showing, the field will be assigned the default value.  On the other hand, if one or more spaces are entered (so the default value is removed) the data entry field will be blank.  If the form is accepted with a blank data entry field, the field will be assigned a `null` value.

|Optional(true)|The annotated field can accept an blank data entry.  If the data entry is blank, the annotated field will be assigned a `null` value.|
|Optional(false)|The annotated field cannot accept just spaces for data entry.|

