The **overall structure and execution flow** of a specific category of software systems can be very similar. The similarity is an opportunity to **reuse** at a high scale.

A _software framework_ is a **reusable implementation of a software**, providing _generic_ functionality that can be selectively customized to produce a _specific_ application.

> [!example]
>  Eclipse is an **IDE framework** that can be used to create IDEs for different programming languages.

Some frameworks provide a **complete implementation** of a _default_ behavior which makes them **immediately usable**.

A framework facilitates the **adaptation and customization** of some desired functionality.

Examples of Frameworks: Eclipse, JavaFX, JUnit

## Differences from [[Libraries]]

- Libraries are meant to be used 'as is', while frameworks are **meant to be customized/extended**. (e.g., add test cases to JUnit)
- Your code calls the library code, while the framework code calls your code. Framework uses *inversion of control* / *"Hollywood principle"* (Dont call us, we'll call you). 
	- e.g. write test methods that will be called by the JUnit framework.
