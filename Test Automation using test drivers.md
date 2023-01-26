**A test driver is the code that ‘drives’ the SUT for the purpose of testing** i.e. invoking the SUT with test inputs and verifying if the behavior is as expected.

```Java
public class PayrollTest {
    public static void main(String[] args) throws Exception {

        // test setup
        Payroll p = new Payroll();

        // test case 1
        p.setEmployees(new String[]{"E001", "E002"});
        // automatically verify the response
        if (p.totalSalary() != 6400) {
            throw new Error("case 1 failed ");
        }

        // test case 2
        p.setEmployees(new String[]{"E001"});
        if (p.totalSalary() != 2300) {
            throw new Error("case 2 failed ");
        }

        // more tests...

        System.out.println("All tests passed");
    }
}
```