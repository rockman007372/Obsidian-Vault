**[[JUnit]] is a tool for automated testing of Java programs.** Similar tools are available for other languages and for automating different types of testing.

```java
@Test
public void testTotalSalary() {
    Payroll p = new Payroll();

    // test case 1
    p.setEmployees(new String[]{"E001", "E002"});
    assertEquals(6400, p.totalSalary());

    // test case 2
    p.setEmployees(new String[]{"E001"});
    assertEquals(2300, p.totalSalary());

    // more tests...
}
```

