TreasureMap
===========

Java library providing simple and standalone use of the JSR-296 ([Swing Application Framework](https://appframework.dev.java.net/)) [ResourceMap](https://appframework.dev.java.net/nonav/javadoc/AppFramework-1.03/org/jdesktop/application/ResourceMap.html) implementation.

Requires Java 1.5 or newer.

Usage
-----

Making the resource map:

``` java
package com.foobar;

import java.util.Locale;

import com.dteoh.treasuremap.ResourceMaps;
import org.jdesktop.application.ResourceMap;

class Foo {
    // Create a ResourceMap for Foo only
    ResourceMap rMap = new ResourceMaps(Foo.class).build();

    // Create a ResourceMap for Bar with Foo's map as the parent
    ResourceMap rMap2 = new ResourceMaps(Bar.class).withParent(rMap).build();

    // Create a ResourceMap for Foo and Bar all in one
    ResourceMap rMapFB = new ResourceMaps(Foo.class).and(Bar.class).build();

    // Create a ResourceMap for RainbowA and RainbowB with a parent map
    ResourceMap rMapWhoa = new ResourceMaps(RainbowA.class).and(RainbowB.class).withParent(rMapFB).build();

    // Create a ResourceMap for the "ABC" Locale
    ResourceMap rMap = new ResourceMaps(Foo.class, new Locale("ABC")).build();
}
```

For the above example, a properties file named "Foo.properties" should be created in the "com.foobar.resources" package as the properties for the Foo class. For the "ABC" locale, a file named "Foo_ABC.properties" should be created.

By default, the builder will create the resource map using the JVM's default locale.

All ResourceMap use patterns are as laid out by the SAF implementation.

Key Differences
---------------

* Extra resource converters: getImage, getDimension
* Explicit locale can be specified
* No need to instantiate the entire application just to load resources. (At the time of writing, BSAF throws a runtime exception if the application is not running. SAF creates a fake application instance.) Not having to instantiate the application allows you to perform unit tests.

License
-------

The library is licensed as [LGPL v2.1](http://www.gnu.org/licenses/lgpl-2.1.html).

Installing
----------

Maven users can add the following dependency:

    <dependency>
        <groupId>com.dteoh</groupId>
        <artifactId>treasuremap</artifactId>
        <version>0.1.1</version>
    </dependency>

