---
layout: default
title: FormField annotation
---
{% include navbar.html parent="documentation" %}

# @{{page.title}}

The `@FormField` annotation adds data entry parameters to Java types.  These parameters are available to built in types as well as custom types.

`@FormField` supports the following parameters:

* "label":#label
* "type":#type
* "length":#length
* "patterm":#pattern
* "message":#message
* "xcase":#xcase
* "sign":#sign
* "precision":#precision
* "scale":#scale
* "min":#min
* "max":#max
* "unique":#unique

## label

A screen label associated with this data entry field. The "label" must be a String.
   
If no "label" is specified, a default label is calculated from the field name using camel case
conventions to break the name into words.  If the field name is "purchaseDate" the field name
will be "Purchase date".  If the field name is "isGSTApplicable" the field label 
will be "Is GST applicable".
   
The screen label can also be calculated at runtime by using the @LableFor annotation on a method.  
The runtime method overrides this parameter.

## type
     
A specified data entry type.  Normally the data entry type is derived from the type of the Java field.
If "type" is specified it replaces the derived type.  "type" must be a Java class that implements 
IType (see "custom types":customTypes.textile).

"type" is used to explicitly specify custom types for common Java fields.  For example, if you write a
customer data entry type for validating payment card numbers, you could write:

<pre><code>@FormField(type=PaymentCardNumberType.class)
String paymentCardNumber;</code></pre>

The data entry type can also be calculated at runtime by using the @TypeFor annotation on a method.  
The runtime method overrides this parameter.
  
## length

For String based types, the maximum length of the string.  The data entry field will only allow "length" number of characters.

The "length" parameter can be used to limit String data entry without having to write a custom type.  For example, if you only want to capture a payment card number without validating it, you could write:

<pre><code>@FormField(length=16)
String paymentCardNumber;</code></pre>

It is also possible to specify a String length using the javax.persistance.Column annotation.
It is an error if both are specified with different "length" values.

Custom types can get access to this parameter by implementing ILengthSettable.
 
## pattern

For String based types, a regular expression that data must match.

The "pattern" parameter can be used to limit String data entry without having to write a custom type.
For example, if you only want to capture a payment card number, checking only that it is made up
of 16 digits, you could write:

<pre><code>@FormField(pattern="^[0-9]{16}$")
String paymentCardNumber;</code></pre>

Custom types can get access to this parameter by implementing IPatternSettable.

## message

For String based types that have a "pattern" parameter, this is the message shown when the data entry does not conform to the pattern.  For example:

<pre><code>@FormField(pattern="^[0-9]{16}$", message="16 digits are required")
String paymentCardNumber;</code></pre>

If a "message" is not specified, the regular expression is displayed as the message.  In the following, the message shown will be "[0-9]{16}".  In most cases, a "message" should be specified when "pattern" is used.

Custom types can get access to this parameter by implementing IPatternSettable.

## xcase

For String based types, the case of the entered characters:

* *TextCase.UPPER* change all entered characters to upper case.
* *TextCase.LOWER* change all entered characters to lower case.
* *TextCase.MIXED* do not change the case of any characters.  This is the default.

If "pattern" is specified, it is possible to derive the case.  For example, the pattern "^[A-Z]*$" will assume "xcase" is TextCase.UPPER.  Deriving the character case from a pattern is not perfect--it may be necessary to also specify "xcase" as well.

This parameter is called "xcase" rather than the more obvious "case" because "case" is a reserved word in Java. 

## sign

For numeric types, whether the entered number can be signed or not:

* *NumberSign.UNSIGNED* the entered number cannot have a sign--positive or negative.
* *NumberSign.SIGNED* the entered number can be preceded with a plus or minus sign.  When displayed (including defaults), negative numbers are preceded with a negative sign, but positive numbers do not have a sign.  This is the conventional handling of signed numbers.
* *NumberSign.RARESIGN* the same as SIGNED, but the length calculation does not include the sign.  The results in a slightly more compact display of signed numbers that are rarely signed.

Custom types can get access to this parameter by implementing ISignAndPrecisionSettable.

## precision

For decimal types, how many digits are allowed to the left of the decimal point.

It is also possible to specify a precision using the javax.persistance.Column annotation.
It is an error if both are specified with different "precision" values.

Custom types can get access to this parameter by implementing ISignAndPrecisionSettable.

## scale

For decimal types, how many digits are allowed to the right of the decimal point.

It is also possible to specify a scale using the javax.persistance.Column annotation.
It is an error if both are specified with different "scale" values.

If not specified, the scale defaults to 0.

Default values used in data entry are displayed with trailing zeros removed from decimal digits.  For example, assume a field with a scale of 2.  If the field has a value of 123.40 the default valuee will be displayed as "123.4".  If the field value is 123.00 the default value will be displayed as "123".

For reports and other display fields, trailing zeros are displayed, up to the number specified by the scale value.

Custom types can get access to this parameter by implementing ISignAndPrecisionSettable.

## min

For integer types, the minimum allowed value.

The "min" and "max" parameter values determine the sign and number of digits allowed but with the additional minimum and maximum value checking.  For example, specifying min=-999 and max=999 is equivalent to sign=SIGNED and precision=3.  Specifying min=0 and max=100 is eqivalent to sign=UNSIGNED and precision=3, but with the additional check that the entered value must be less than or equal to 100.

Either "min" and "max" or "sign" and "precision" parameter values can be used on an integer field, but not both.

Custom types can get access to this parameter by implementing IMinMaxSettable.

## max

For integer types, the maximum allowed value.  See the description of "<a href='#min'>min</a>" parameter above.

Custom types can get access to this parameter by implementing IMinMaxSettable.

## unique

Obsolete.  No longer used.
