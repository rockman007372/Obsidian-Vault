
Three axioms of functional dependency

1. Axiom of **Reflexivity**: ABC → AB → A
2. Axiom of **Augmentation**: A → B ⇒ AC → BC
3. Axiom of **Transitivity**: (A → B) & (B → C) ⇒ A → C

### Additional Rule

- Rule of **Decomposition**: If A → BC, then A → B and A → C

> [!proof]
> 1. BC → B (reflexivity)
> 2. A → BC and BC → B ⇒ A → B (transitivity)

- Rule of **Union**: If A → B and A → C, then A → BC

>[!proof]
> 1. A → B ⇒ A → AB (augmentation)
> 2. A → C ⇒ AB → BC (augmentation)
> 3. Hence A → BC (transitivity)


> [!note]
> The rule of decomposition is the **converse** of the rule of union.