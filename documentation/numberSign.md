---
layout: default
title: Number sign
---
<!--
{% include navbar.html parent="documentation" %}

<div id="toc" class="pull-right">
* Documentation
** "Built-in types(Java types that are supported out of the box)":builtinTypes
** "Annotations(How annotations can be used to enhance field validation)":annotations
** "Defaults(How defaults can be specified as initial values or calculated at runtime)":defaults
</div>
-->

{{page.title}}
==============

Whether an data entry field can be signed or not.

SIGNED
: Conventional signed number.  On data entry, a sign (+ or -) can be entered.  Entry of a + sign for positive numbers is optional.

UNSIGNED
: Conventional unsigned number.  On data entry, no sign can be entered.  Even for positive numbers, the + sign cannot be entered.

When displaying values the conventional rules apply.  Negative numbers are displayed with a leading minus sign.  Zero and positive numbers are displayed without a sign.

Values can also be displayed in other formats.  For example, when displaying values on financial reports, negative numbers are displayed with surrounding parentheses () while zero and positive numbers are displayed without parentheses. 

There is an enumeration `NumberSign` that is used for the data entry sign:

~~~ java
public enum NumberSign {

  SIGNED,		// + or - sign can be used
  UNSIGNED;		// no sign can be entered
}
~~~
