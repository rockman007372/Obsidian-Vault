> [!definition]
> **Unit testing**: testing individual units (methods, classes, subsystems, ...) to ensure each piece works correctly.

In OOP code, it is common to write one or more unit tests for **each public method of a class**.

```java
class Foo {
    String read() {
        // ...
    }
    
    void write(String input) {
        // ...
    }
    
}
```

```java
class FooTest {
    
    @Test
    void read() {
        // a unit test for Foo#read() method
    }
    
    @Test
    void write_emptyInput_exceptionThrown() {
        // a unit tests for Foo#write(String) method
    }  
    
    @Test
    void write_normalInput_writtenCorrectly() {
        // another unit tests for Foo#write(String) method
    }
}
```

**A proper unit test requires the _unit_ to be tested in isolation** so that bugs in the dependencies cannot influence the test i.e. bugs outside of the unit should not affect the unit tests.

**_[[Stubs]]_ can isolate the SUT from its dependencies**.