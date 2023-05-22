---
alias: equivalence partitions
---

>[!definition]
>   **Equivalence partition (aka equivalence class)**: A group of test inputs that are likely to be processed by the SUT in the same way.

**By dividing possible inputs into equivalence partitions you can,**

-   **avoid testing too many inputs from one partition.** Testing too many inputs from the same partition is unlikely to find new bugs. This increases the efficiency of testing by reducing redundant test cases.
-   **ensure all partitions are tested.** Missing partitions can result in bugs going unnoticed. This increases the effectiveness of testing by increasing the chance of finding bugs.

## How to do EP

When deciding EPs of OOP methods, you need to identify the EPs of **all data participants** that can potentially influence the behaviour of the method, such as,

-   the **target object** of the method call
-   **input parameters** of the method call
-   other data/objects accessed by the method such as **global variables**. This category may not be applicable if using the black box approach (because the test case designer using the black box approach will not know how the method is implemented).

> [!Example]
> Consider the `Logic` component of the Minesweeper application. 
> 
> What are the EPs for the `markCellAt(int x, int y)` method? The partitions in **bold** represent valid inputs.
> -   `Logic`: PRE_GAME, **READY**, **IN_PLAY**, WON, LOST
> -   `x`: [MIN_INT..-1] **[0..(W-1)]** [W..MAX_INT] (assuming a minefield size of WxH)
> -   `y`: [MIN_INT..-1] **[0..(H-1)]** [H..MAX_INT]
> -   `Cell` at `(x,y)`: **HIDDEN**, MARKED, CLEARED