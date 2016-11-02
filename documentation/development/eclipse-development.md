---
layout: default
title: Eclipse IDE
---
{% include navbar.html parent="documentation" %}

<div id="toc" class="pull-right">
* Development
** Eclipse IDE
</div>

# {{page.title}}

Eclipse is used a the development environment for all PennyLedger code.

"Eclipse Mars.2 (4.5.2)" is used.  This is currently the latest stable version.  There is nothing about Neon (4.6) that will require its use, so it is likely the Mars version will be used for some time.

The "Eclipse IDE for Java EE Developers" package is used.

## Additional software for development

For development, the following software is added to the "Java EE Developers" package:

* com.wuetherich.osgi.ds.annotations.feature	1.1.5.201411080545
* EclEmma Java Code Coverage	2.3.2.201409141915

The above software is installed using the Help/Install New Software menu item.
 
## Additional software for runtime

The following software is added to the "dropins" directory of Eclipse.  This software is used at runtime.


