---
layout: default
title: Entry mode
---
{% include navbar.html parent="documentation" %}

<div id="toc" class="pull-right">
* Documentation
** "Built-in types(Java types that are supported out of the box)":builtinTypes
** "Annotations(How annotations can be used to enhance field validation)":annotations
** "Defaults(How defaults can be specified as initial values or calculated at runtime)":defaults
</div>

# {{page.title}}

Whether an data entry field allows data entry, is view only, or is not applicable to the form.

There is an enumeration "EntryMode" that is used for data entry mode:

* EntryMode.ENTRY := Normal data entry is allowed.
* EntryMode.VIEW := The value of the data entry field is displayed but no changes can be made.
* EntryMode.NA := The data entry field is not applicable in this form.  For example, if a form has a checkbox for "isTaxApplicable", a tax rate field would be not applicable if this checkbox was clear.

If an entry field is not applicable, the field and field label are not shown--they occupy no space of the form.
^

## Example

{% highlight java %}
public class DataEntryForm {

  @FormField(mode=EntryMode.ENTRY, length=5)
  private String locationCode;
  
  @FormField(mode=EntryMode.VIEW)
  private String locationName;
  
  private boolean difficultDelivery;
  
  private double deliveryCost;
  
  // ... other logic
  
  @ModeFor("deliveryCost")
  private EntryMode deliveryCostMode () {
    if (difficultDelivery) {
      return EntryMode.ENTRY;
    } else {
      return EntryMode.NA;
    }
  }
  
}
{% endhighlight %}

`locationCode` is a conventional data entry field.  In this example it is 5 characters in length.

`locationName` is a conventional view or display field.  It is assumed there is some logic (not shown) that retrieves the location name when a location code is entered.

`deliveryCostMode` is a method that returns the entry mode for `deliveryCost`.  If `difficultDelivery` is entered as true (the boolean checkbox is checked), the entry mode for `deliveryCost` will be `EntryMode.ENTRY`.  That is, `deliveryCost` will be a conventional data entry field.  If, however, `difficultDelivery` is entered as false (the boolean checkbox is clear), the entr mode for `deliveryCost` will be `EntryMode.NA`.  In tis case, `deliveryCost` (and its associated label) will not be shown at all.
