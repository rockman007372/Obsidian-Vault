
>[!Definition]
> Two relation R and S are union-compatible if it satisfies both of the following:
> - R and S have the same number of attributes
> - The corresponding attributes have the same or compatible domains

- Just because 2 relations are union-compatible, does not mean the set operation is meaningful.
- Example of union-compatible relations:

```sql
Employees(name: TEXT. role: TEXT, age: INT)
Teams(ename: TEXT, pname: TEXT, hours: INT)
```