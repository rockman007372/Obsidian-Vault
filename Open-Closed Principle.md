	 ## Open-Closed Principle

>[!definition]
> **Open-closed principle (OCP)**: A module should be _open_ for extension but _closed_ for modification. That is, modules should be written so that they can be extended, without requiring them to be modified.

The Open-Closed Principle aims to make a code entity **easy to adapt and reuse without needing to modify** the code entity itself.

## How to use OCP?

### Generics

>[!Example]
> In the code below, the `ArrayList` class behaves as a container of `Students` in one instance and as a container of `Admin` objects in the other instance, without having to change its code. That is, the behavior of the `ArrayList` class is extended without modifying its code.

```java
ArrayList students = new ArrayList<Student>();
ArrayList admins = new ArrayList<Admin>();
```

### Interface

Interface allows different implementations of the same methods (Open) without changing the methods defined in the interface (Closed)

Iconic example of OCP: Shape and Area

```java

public interface Shape {
	getArea();
}

public class AreaCalculator {
	
	public double calculateArea(Shape[] shapes)
		double area = 0;
		for (Shape shape : shapes) {
			area += shape.getArea();
		}
		return area;
}
```