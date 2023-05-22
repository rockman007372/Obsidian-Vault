>[!definition]
>**Stub**: A stub has the same interface as the component it replaces, but its implementation is so simple that it is unlikely to have any bugs. 

It mimics the responses of the component, but only for a limited set of predetermined inputs. That is, it does not know how to respond to any other inputs. 

Typically, these mimicked responses are **hard-coded in the stub rather than computed or retrieved from elsewhere**, e.g. from a database.

Given the classes below:

```Java
class Logic {
    Storage s;

    Logic(Storage s) {
        this.s = s;
    }

    String getName(int index) {
        return "Name: " + s.getName(index);
    }
}
```

```Java
interface Storage {
    String getName(int index);
}
```

```Java
class DatabaseStorage implements Storage {

    @Override
    public String getName(int index) {
        return readValueFromDatabase(index);
    }

    private String readValueFromDatabase(int index) {
        // retrieve name from the database
    }
}
```

Unit test:

```Java
@Test
void getName() {
    Logic logic = new Logic(new DatabaseStorage());
    assertEquals("Name: John", logic.getName(5));
}
```

However, this `logic` object being tested is making use of a `DataBaseStorage` object which means a bug in the `DatabaseStorage` class can affect the test. Therefore, this test is not testing `Logic` _in isolation from its dependencies_ and hence it is not a pure unit test.

Here is a stub class you can use in place of `DatabaseStorage`:

```Java
class StorageStub implements Storage {

    @Override
    public String getName(int index) {
        if (index == 5) {
            return "Adam";
        } else {
            throw new UnsupportedOperationException();
        }
    }
}
```

Here is how you can use the stub to write a unit test. This test is not affected by any bugs in the `DatabaseStorage` class and hence is a pure unit test.

```Java
@Test
void getName() {
    Logic logic = new Logic(new StorageStub());
    assertEquals("Name: Adam", logic.getName(5));
}
```
