---
layout: default
title: Built-in types
---
<!--
{% include navbar.html parent="documentation" %}

<div id="toc" class="pull-right">
  <p>Documentation</p>
  <ul>
    <li>"Built-in types(Java types that are supported out of the
      box)":builtinTypes</li>
    <li>Annotations(How annotations can be used to enhance field
      validation)":annotations</li>
    <li>"Defaults(How defaults can be specified as initial values
      or calculated at runtime)":defaults</li>
  </ul>
</div>
-->

{{page.title}}
==============

Out-of-the-box data types that are supported by j2form:

* Primitive Java types and their corresponding wrapper types
* String
* Date based types
* BigDecimal, BigInteger and Decimal
* URL and email address
* File and directory
* Locale

Custom data types can also be specified.

Primitive Java types and their corresponding wrapper types
==========================================================

j2form supports all of the Java primitive types and corresponding wrapper types:

char
: A one character data entry field. `char` types can be annotated with the "pattern" attribute of @FormField to limit what characters are entered.=:

int
: By default, an 11 character data entry field that accepts a number in the range =2147483648 to 2147483647.

  `int` types can be annotated using @FormField with attributes as follows:

  |_. @FormField@ attributes|_. Effect|
  |@min@ and @max@|The entered value must be between the @min@ and @max@ values, inclusive.  The data entry field length will be the number of characters that allow entry of such values.  The data entry value will be UNSIGNED if the @min@ value is zero or positive, and SIGNED otherwise.  If UNSIGNED, no sign may be entered.|
  |@sign@ and @precision@|The entered value must contain no more than @precision@ digits  If @sign@ is SIGNED or RARE_SIGN, a sign my precede the digits.  If UNSIGNED, no sign may be entered.
  |@length@|The entered value must contain no more than @length@ digits.  The entered value is assumed to be UNSIGNED.|

byte
: By default, a 4 character field that accepts a number in the range -128 to 127. `byte` types can be annotated using @FormField in the same way as the `int` type described above.

short
: By default, a 6 character data entry field that accepts a number in the range -32768 to 32767. `short` types can be annotated using @FormField in the same way as the `int` type described above.

long
: By default, a 20 character data entry field that accepts a number in the approximate range &plusmn;9x10<sup>18</sup>. `long` types can be annotated using `@FormField` in the same way as the `int` type described above.

double
: By default, a ? character field that accepts a signed decimal number, with no decimal digits. This allows for a number in 
  the range &plusmn;999999. Exponential format numbers (such as 1E20), &plusmn;infinity and NaN cannot be entered.  

 `double` types can be annotated using @FormField with the "sign", "precision" and "scale" set. If these attributes are set,
  this will determine the length of the data entry field. The "min" and "max" attributes cannot be used.
  
float
: By default, a ? character field that accepts a signed decimal number, with no decimal digits. This allows for a number
  int the range &plusmn;99999. `float` types can be annotated using @FormField in the same as the `double` type described above.

boolean
: A checkbox that can be checked or un-checked. If checked, the boolean value is `true`. If un-checked, the 
  boolean value is `false`. There are no attributes of @FormField that apply to the `boolean` type.

None of the primitive types can be optional. By definition, they cannot be @null@.


The Java wrapper types--Character, Integer, Long, Byte, Double,
Float and Boolean--are all supported. The field length and validation
are the same as the corresponding primitive types. The only difference
between the two is that the wrapper types can be optional. If a
wrapper type is annotated as Optional, and nothing is entered in the
data entry field, the field value will be `null`.

All of the numeric types accept locale specific grouping
separators. For example (in most English locales) `1,000,000`. This
allows you to cut and paste numbers displayed with grouping
separators.

All of the decimal types use the locale specific decimal
character.

String
======


