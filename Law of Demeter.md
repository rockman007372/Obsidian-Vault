## Law of Demeter

>[!definition]
> **Law of Demeter (LoD)**:
> - An object should have limited knowledge of another object.
> - An object should only interact with objects that are closely related to it.

Also known as
-   Don’t talk to strangers.
-   Principle of least knowledge

More concretely, a method `m` of an object `O` should invoke only the **methods** of the following kinds of objects:
-   The object `O` itself
-   Objects passed as parameters of `m`
-   Objects created/instantiated in `m` (directly or indirectly)
-   Objects from the direct association of  `O`

**LoD aims to prevent objects from navigating the internal structures of other objects.** This reduces coupling.

> [!example]
> The following code fragment violates LoD due to the following reason: while `b` is a ‘friend’ of `foo` (because it receives it as a parameter), `g` is a ‘friend of a friend’ (which should be considered a ‘stranger’), and `g.doSomething()` is analogous to ‘talking to a stranger’.

```java
void foo(Bar b) {
    Goo g = b.getGoo();
    g.doSomething(); // violates LOD
}
```