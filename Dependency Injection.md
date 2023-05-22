**_Dependency injection_ is the process of 'injecting' objects to replace current dependencies with a different object.** This is often used to inject [[Stubs]] to isolate the SUT from its dependencies so that it can be tested in isolation.

>[!example]
> A `Foo` object normally depends on a `Bar` object, but you can inject a `BarStub` object so that the `Foo` object no longer depends on a `Bar` object. Now you can test the `Foo` object in isolation from the `Bar` object.

![](https://nus-cs2103-ay2223s2.github.io/website/book/testing/dependencyInjection/what/images/diagram.png)

## How to perform dependency Injection

You can make use of [[Polymorphism]] to inject stubs. 

For example, the method `Payroll::setSalaryManager(SalaryManager)` takes in an instance of `SalaryManager` as argument. You can make a `SalaryManagerStub` which **inherits** from `SalaryManager` amd inject the stub into the function.

```java
class Payroll {
    private SalaryManager manager = new SalaryManager();
    private String[] employees;

    void setEmployees(String[] employees) {
        this.employees = employees;
    }

    void setSalaryManager(SalaryManager sm) {
        this.manager = sm;
    }

    double totalSalary() {
        double total = 0;
        for (int i = 0; i < employees.length; i++) {
            total += manager.getSalaryForEmployee(employees[i]);
        }
        return total;
    }
}
```

```java
class SalaryManager {
    double getSalaryForEmployee(String empID) {
        // code to access employee’s salary history
        // code to calculate total salary paid and return it
    }
}

class SalaryManagerStub extends SalaryManager { 
	/** Returns hard coded values used for testing */ 
	double getSalaryForEmployee(String empID) { 
		if (empID.equals("E001")) 
			{ return 1000.0; 
		} else if (empID.equals("E002")) { 
			return 1500.0; 
		} else { 
			throw new Error("unknown id"); 
		} 
	} 
}
```
