**Test cases need to be designed to make the best use of testing resources.** In particular:

-   **Testing should be _effective_** i.e., it finds a high percentage of existing bugs e.g., a set of test cases that finds 60 defects is more effective than a set that finds only 30 defects in the same system.
    
-   **Testing should be _efficient_** i.e., it has a high rate of success (bugs found/test cases) a set of 20 test cases that finds 8 defects is more efficient than another set of 40 test cases that finds the same 8 defects.

For testing to be E&E, each new test you add should be **targeting a potential fault that is not already targeted by existing test cases.** There are test case design techniques that can help us improve the E&E of testing.

## Black Box vs White Box vs Grey Box

-   **_Black-box_ (aka _specification-based or responsibility-based_) approach**: test cases are designed exclusively based on the SUT’s specified external behavior. (For testers that are not developers)

-   **_White-box_ (aka _glass-box or structured or implementation-based_) approach**: test cases are designed based on what is known about the SUT’s implementation, i.e. the code. (For developers)
   
-   **_Gray-box_ approach**: test case design uses _some_ important information about the implementation.

## Techniques to improve E&E

- [[Equivalence Partitioning]]
- [[Boundary Value Analysis]]
- [[Combining Test Inputs]]

## Other QA Techniques

- [[Validation versus Verification]]
- [[Formal Verification]]