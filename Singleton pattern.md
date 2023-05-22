## Context

Certain classes should have no more than just one instance (e.g. the main controller class of the system). These single instances are commonly known as _singletons_.

## Problem

A normal class can be instantiated multiple times by invoking the constructor.

## Solution

1. Make the constructor of the singleton class `private`, because a `public` constructor will allow others to instantiate the class at will. 
2. Provide a `public` class-level method to access the _single instance_.

```JAVA
class Logic {
    private static Logic theOne = null;

    private Logic() {
        ...
    }

    public static Logic getInstance() {
        if (theOne == null) {
            theOne = new Logic();
        }
        return theOne;
    }
}
```

## Limitations

-   The singleton object acts like a global variable that **increases coupling** across the code base.
- Testing difficulties:
	-   difficult to replace Singleton objects with stubs (static methods cannot be overridden).
	-   singleton objects carry data from one test to another even when you want each test to be independent of the others.