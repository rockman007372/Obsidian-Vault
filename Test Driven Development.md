**_Test-Driven Development(TDD)_ advocates writing the tests before writing the SUT, while evolving functionality and tests in small increments**. In TDD you first define the precise behavior of the SUT using test code, and then update the SUT to match the specified behavior. One big advantage of TDD is that it guarantees the code is testable.

Note that TDD does not imply writing all the test cases first before writing functional code. Rather, proceed in small steps:

1.  Decide what behavior to implement.
2.  Write/modify a test case to test that behavior.
3.  Run the test cases and watch them fail.
4.  Implement the behavior.
5.  Run the test cases.
6.  Keep modifying the code and rerunning test cases until they all pass.
7.  Refactor code to improve quality.
8.  Repeat the cycle for each small unit of behavior that needs to be implemented.

Some TDD proponents cite the following as the three rules of TDD, that once again emphasize the need to proceed in very small steps:

1.  You are not allowed to write any production code unless it is to make a failing unit test pass.
2.  You are not allowed to write any more of a unit test than is sufficient to fail; and compilation failures are failures.
3.  You are not allowed to write any more production code than is sufficient to pass the one failing unit test.