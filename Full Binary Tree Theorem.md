2022-06-22 01:21
Tags: [[Data Structure and Algorithm]] #flashcards
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   

> [!terms]
>i = the number of internal nodes
>n = be the total number of nodes
>l = number of leaves
>λ = number of levels

>[!theorem]
> 1. The number of leaves is: `i + 1`.
> 2. The total number of nodes is: `2i + 1`.
> 3. The number of internal nodes is: `(n – 1) / 2`.
> 4. The number of leaves is: `(n + 1) / 2`.
> 5. The total number of nodes is: `2l – 1`.
> 6. The number of internal nodes is: `l – 1`.
> 7. The number of leaves is at most: `2λ - 1`.

---

Let n = number of nodes, h = height of tree

>[!theorem]
>n = $2^h + 1$
>h = lg(n - 1) 