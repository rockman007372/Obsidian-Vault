**An SUT can take multiple inputs.** You can select values for each input (using [[Equivalence Partitioning|equivalence partitioning]], [[Boundary Value Analysis|boundary value analysis]], or some other technique).

Testing all possible combinations is effective but not efficient. Therefore, **we need smarter ways to combine test inputs that are both effective and efficient.**

## Test Input Combination Strategies

1. All-combinations strategy: each unique combination
2. At-least-once strategy: includes each test input at least once.
3. All-pairs strategy: for any given pair of inputs, all combinations between them are tested. Based on the observation that a bug is rarely a result of more than 2 interacting factors. More test cases that at-least-once, but less than all-combination approach.

## Heuristics

Example: `printLabel(String fruitName, int unitPrice)`

These following test cases violate 2 heuristics:

| Case | Fruit      | unitPrice | Expected                       |
| ---- | ---------- | --------- | ------------------------------ |
| 1    | Apple      | 1         | Print label                    |
| 2    | Banana     | 20        | Print label                    |
| 3    | Cherry     | <u>0</u>         | Error message: "invalid price" |
| 4    | <u>Dog</u>        | <u>-1</u>        | Error message: "invalid fruit" | 


**1. Each valid input at least once in a positive test case**

Cherry is a valid input, but it is in a negative test case. Hence we cannot test the validitiy of Cherry.

**2. No more than one invalid input in a test case**

Dog and -1 are both invalid inputs. Hence we cannot test which one causes the error message. 



