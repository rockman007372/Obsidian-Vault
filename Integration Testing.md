>[!definition]
> Integration testing: testing whether different parts of the software _work together_ (i.e. integrates) as expected.

> [!Example]
> Suppose a class `Car` uses classes `Engine` and `Wheel`. If the `Car` class assumed a `Wheel` can support a speed of up to 200 mph but the actual `Wheel` can only support a speed of up to 150 mph, it is the integration test that is supposed to uncover this discrepancy.

**Integration testing is not simply a case of repeating the unit test cases using the actual dependencies** (instead of the stubs used in unit testing). Instead, integration tests are additional test cases that focus on the interactions between the parts.

Suppose a class `Car` uses classes `Engine` and `Wheel`. Here is how you would go about doing pure integration tests:

a) First, unit test `Engine` and `Wheel`.  
b) Next, unit test `Car` in isolation of `Engine` and `Wheel`, using [[Stubs]] for `Engine` and `Wheel`.  
c) After that, do an integration test for `Car` by using it together with the `Engine` and `Wheel` classes to ensure that `Car` integrates properly with the `Engine` and the `Wheel`.

**In practice, developers often use a hybrid of unit+integration tests to minimize the need for stubs.** That is, they skip step b above.