---
layout: default
title: j2form documentation
---
<!--
{% include navbar.html here="documentation" %}
-->

Documentation
=============

j2form takes an ordinary Java class and produces a data entry form.  The form handles all the data entry validation, including inter-field validation.  The form handles all the Java types you would expect, such as:
* Strings
* Integers
* Floating point and decimal numbers
* Booleans
* Enumerated types
* Dates
* URL's
* File and directory names

j2form also handles custom types, lists and arrays, embedded classes, references to other classes, and interfaces.

Default values are supported.  They can be specified as initial field values, or calculated at runtime.

A very simple example is:

~~~ java
public class Invoice {

  private Date purchaseDate = new Date();
  
  private Double amount;
  
  private String paymentCardNumber;
  
  private boolean gstApplicable;

  public Date getPurchaseDate() {
    return purchaseDate;
  }
  
  public Double getAmount() {
    return amount;
  }
  
  public String getPaymentCardNumber() {
    return paymentCardNumber;
  }
  
  public boolean getGstApplicable();
    return getApplicable;
  }
}
~~~

With j2form, the following data entry form is produced:

[image of Invoice.java data entry form]

The *Purchase date* field shows the default value of "today".  This is from the code <code>= new Date()</code>. 

"Annotations are available(the full list of form annotations)":annotations to enhance the data entry form.  One of these is the "@FormField(more information on the @FormField annotation)":formFieldAnnotation.  The @FormField annotation specifies:

* A field length and  regular expression pattern for Strings.
* The allowed sign and number of whole and decimal digits for Double, Float and other decimal types.
* The minimum and maximum for integer types.
* Other more advanced options.

A second example that includes @FormField annotations and a list.

~~~ java
public class Item {
  @FormField(length=6)
  private String itemNumber;
  
  private double cost;
  
  @FormField(min=0, max=999)
  private int quantity;
  
  // getter methods omitted
}
~~~
  
~~~ java
public class Invoice {

  private Date purchaseDate = new Date();
  
  @FormField(sign=
  private Double amount;
  
  @FormField(regex="^[0-9 ]$", message="Only digits and spaces are allowed")
  private String paymentCardNumber;
  
  private boolean gstApplicable;

  private List<Item> itemsPurchased;
  
  // getter methods omitted
  
  private void checkCardDigits () throws UserEntryException {
    int n = 0;
    for (int i = 0; i < paymentCardNumber.length(); i++) {
      char c = paymentCardNumber.charAt(i);
      if (Character.isDigit(c)) {
        n++;
      }
    }
    if (n < 16) {
      throw new UserEntryException("16 digits are required", INCOMPLETE);
    } else if (n > 16) {
      throw new UserEntryException("only 16 digits are required", ERROR);
    }
  }
  
}
~~~

"Custom types(more information on custom types)":customTypes.textile can also be used.

Note the validation method *checkCardDigits*. j2form can determine that this method is depend on *paymentCardNumber*, and will call this method whenever *paymentCardNumber* changes.  The user will see and incomplete icon if the number of digits is less than 16, and will see an error icon if the number of digits is greater than 16.  See "Validation(more information on validation)":validation.textile for how j2form validates user entry, and how validation methods are called.
