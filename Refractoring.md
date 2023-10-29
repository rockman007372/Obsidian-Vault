---
tags: toProcess, swe
course: CS2103T
date: 2023-02-12 Sunday
---

>[!proper definition]
> The process of improving a program's internal structure in small steps without modifying its external behavior.

Characteristics:

- **Refactoring is not rewriting**: Discarding poorly-written code entirely and re-writing it from scratch is not refactoring because refactoring needs to be done in small steps.
- **Refactoring is not bug fixing**: By definition, refactoring is different from bug fixing or any other modifications that alter the external behavior (e.g. adding a feature) of the component in concern.

All thing related to refractoring can be found [here](https://refactoring.guru/refactoring).

Common refractoring techniques are [here](https://refactoring.com/catalog/).

## Examples

Refactoring Name: **Consolidate Duplicate Conditional Fragments**

- Situation: The same fragment of code is in all branches of a conditional expression.
- Method: Move it outside of the expression.
- Example:

```java
if (isSpecialDeal()) {
    total = price * 0.95;
    send();
} else {
    total = price * 0.98;
    send();
}
```

```java
if (isSpecialDeal()) {
    total = price * 0.95;
} else {
    total = price * 0.98;
}
send();
```

Refactoring Name: **Extract Method**

- Situation: You have a code fragment that can be grouped together.
- Method: Turn the fragment into a method whose name explains the purpose of the method.
- Example:

```java
void printOwing() {
    printBanner();

    // print details
    System.out.println("name:	" + name);
    System.out.println("amount	" + getOutstanding());
}
```

```java
void printOwing() {
    printBanner();
    printDetails(getOutstanding());
}

void printDetails(double outstanding) {
    System.out.println("name:	" + name);
    System.out.println("amount	" + outstanding);
```



---
Links: [[CS2103T]]
