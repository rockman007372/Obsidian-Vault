## Liskov Substitution Principle

>[!definition]
> **Liskov substitution principle (LSP)**: Derived classes must be substitutable for their base classes.

**LSP implies that a subclass should not be more restrictive than the behavior specified by the superclass.** If a class B is substitutable for a parent class A, then it should be able to pass all test casese of parent class A.

If LSP is not followed, substituting a subclass object for a superclass object can break the functionality of the code.

Example: 

If time is between 10am and 11am, `RestaurantWeekend` behaves differently from its parent.

```java

class Restaurant {
	public boolean isOpen(DateTime time) {
		if (time > DateTime.parse("10am")) {
			return true;
		} 
		return false;
	}
}

class RestaurantWeekend extends Restaurant {
	@Override
	public boolean isOpen(DateTime time) {
		if (time > DateTime.parse("11am")) { 
			return true;
		} 
		return false;
	}
}
```