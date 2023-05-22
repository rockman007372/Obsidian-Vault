## Class Diagram

- Default visibility in JAVA is **package private**: ~. However, Java interface methods are **public** by default
- No need to show aggregation (container). However, must have composition (whole part relationship)
- Watch out for **dependency** in class diagram (return type, argument, static attributes...)
- Two **unidirectional** associations in opposite directions do not add up to a single **bidirectional** association (owner:Person -> :Cat vs :Cat -> breeder:Person)
- abstract classes and methods are indicated as {abstract} or *abstract*
- If an abstract class inherits from an interface with an abstract method, **you dont need to include the method if the class does not implement it**
- Concrete classes must implement abstract methods it inherits from interface/abstract parent classes ⇒ must draw methods in class diagram

## Object Diagram

- No dependency in object diagram!
- No compartment for method in **object** diagram (object diagram has no methods)
- No multiplicities
- Object diagram may have navigability (> arrow heads)
- **the object diagram should show either an object of the parent class or the child class, but not both**.

## Sequence Diagram

- In sequence diagram, an object existing earlier will be **higher** than an object existing later
- ? A loop can execute 0 times, hence should be included in sequence
- Its fine to obmit activation bars, **even for constructors**
- Can obmit return arrow!
- In sequence diagram, replace `this` with the name of the object calling the function
- In sequence diagram, an object can call the method belonging to another object. However, that method does not belong to the caller.
- Conditions in sequence diagram must be in **square brackets**
- `<<Class>>` to indicate class/static methods in sequence diagram. Does not have ":" since its not an instance
- If there are different **return** statements inside different branches, must include them all inside their alt paths
- If there is only one if statement, it is an **Opt frame** instead of an Alt frame!


## OODM

- For domain-modeling, we should use OODMs instead of class diagrams 
- **No navigability** in OODMs
- No internal classes. No methods.
- OODM can have properties/attributes (just not methods and navigability)

## Use Case

- In Use Case diagram, the direction of the arrow is from the **extension** to the use case it extends and the arrow uses a **dashed line.**

![[Pasted image 20230424183610.png|450]]
- **A use case can include another use case.** Underlined text is used to show an inclusion of a use case.
- Inclusion can be shown using dotted line and `<<include>>`. Direction of arrow is reverse from `<<extend>>` arrow
- Do not include system into use case (system is not a user). Limit use cases for modeling behaviors that involve an external actor.

## Test cases

- Take note of boundary partition, boundary values and non-boundary values. You should only have 1 non-boundary value in one partition
- Where there is a loop, we must go through every iteration of the loop to achieve 100% **path coverage**

## Designs

- 3 design fundamentals: abstraction, coupling, cohesion
- 2 approaches to integration frequency: **late and one time** vs **early and frequent**
- 2 approaches to integration method: big-bang (all components integrated) vs incremental (integrate components one by one)

## Activity Diagram

- Acceptable simplifications of branch node in activity diagram: no merge node, arrow start from same corner of branch node, no else condition

![[Pasted image 20230425130536.png]]
- Guard condition must be in **square brackets** (easily missed!!!)
- In activity diagram, some condition may overlap! If condition B is met, condition A is also met => **cannot draw them both from one branch node**, but must separate into 2 branch node!

![[Pasted image 20230425131851.png]]

## Miscellaneous

- Coding quality vs Coding standard! (magic number is not a code standard problem)
- Gradle is not a CI (Continuous Integration) platform. GitHub Action is a CI platform. Gradle is a build tool. CI platform uses build tools to perform build task.
- [[Checked Exception vs Unchecked Exception]].  Checked exception can go through methods