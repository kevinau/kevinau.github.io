---
layout: documentation
title: Built-in types
---

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

# {{page.title}}

* Primitive Java types and their corresponding wrapper types
* String based types
* Date based types
* BigDecimal, BigInteger and Decimal
* URL and email address
* File and directory
* Locale

## Primitive Java types and their corresponding wrapper types {#primitive}

j2form supports all of the Java primitive types:

char
:   A one character data entry field. `char` types can be
    annotated with the "pattern" attribute of @FormField to limit what
    characters are entered.

int
:   By default, an 11 character data entry field that accepts a
    number in the range =2147483648 to 2147483647. `int` types can be
    annotated using @FormField with the "min" and "max" attributes
    set. If the "min" and "max" attributes are set, this will determine
    the length of the data entry field. The "sign" and "precision"
    attributes can be set in place of the "min" and "max" attributes.

byte
:   By default, a 4 character field that accepts a number in the
    range -128 to 127. `byte` types can be annotated using @FormField
    in the same way as the `int` type described above.

`short`
:   By default, a 6 character data entry field that accepts a
    number in the range -32768 to 32767. `short` types can be annotated
    using @FormField in the same way as the `int` type described
    above.

long
:   By default, a 20 character data entry field that accepts a
    number in the range -9223372036854775808 to 9223372036854775807.
    `long` types can be annotated using `@FormField` in the same way as
    the `int` type described above.

double
:   By default, a ? character field that accepts a signed decimal
    number, with no decimal digits. This allows for a number in the
    range &plusmn;999999. `double` types can be annotated using
    @FormField with the "sign", "precision" and "scale" set. If these
    attributes are set, this will determine the length of the data entry
    field. The "min" and "max" attributes cannot be used. Exponential
    format numbers (such as 1E20), &plusmn;infinity and NaN cannot be
    entered.

float
:   By default, a ? character field that accepts a signed decimal
    number, with no decimal digits. This allows for a number int the
    range &plusmn;99999. `float` types can be annotated using
    @FormField in the same as the `double` type described above.

boolean
:   A checkbox that can be checked or un-checked. If checked, the
    boolean value is `true`. If un-checked, the boolean value is
    `false`. There are no attributes of @FormField that apply to the
    `boolean` type.

None of the primitive types can be optional. By definition, they
cannot be null.
  
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

## String based types {#stringBased}


