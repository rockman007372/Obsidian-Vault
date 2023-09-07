---
alias: Prime Attribute
---

## Definition

- A prime attribute is one of the attributes that make up the [[Candidate Keys]]. If an attribute appears in a key, it is a prime attribute.
- Together, they can be used to uniquely identify a tuple in the schema.

## Example

Suppose we have a table of customers with the following attributes:
- `customer_id, first_name, last_name, email, phone_number `
- If we choose `customer_id` as the primary key, then `customer_id` is a prime attribute. 
- If we choose a composite key consisting of `first_name, last_name, email`, then all three attributes are prime attributes.