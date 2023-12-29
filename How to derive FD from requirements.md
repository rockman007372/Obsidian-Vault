
>[!tip]
> The attribute that **cannot** violate a **one-to-many** relationship is the attribute on the left.

Lets say we have table:

```sql
Purchase(CustomerID, ProductID, ShopID, Price, Date)
```

**Example 1:** Each shop can sell at most one product
FD: ShopID -> ProductID

| shop | product |
| ---- | ------- |
| s1   | p1      |
| s1   | p2      |

Since S cannot violates one-to-many relationship, S -> P

**Example 2:** No two shops sell the same product
FD: ProductID -> Shops

**Example 3:** No two customers can buy the same product
FD: ProductID -> CustomerID

**Example 4:** No 2 shops sell the same product on the same day
FD: ProductID, Date -> ShopID

**Example 5:** No shop should sell the same product to the same customer on the same date at two different prices.
FD: Shop, Product, Customer, Date -> Price

