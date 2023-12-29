
If a table is in BCNF:
- Any attribute that is not part of any superkeys, can only depend on the superkeys.
- Any dependency on non-superkeys is prohibited.

Why does this matter?
- Suppose B depends on non-superkey C, e.g. C → B
- Since C is not a superkey, the same C can be repeated in the table
- Hence, whenever C appears, the same B must appear as well.
- This leads to **redundancy**

| A   | B   | C   |
| --- | --- | --- |
| A1  | B1  | C1  |
| A2  | B1  | C1  |
| A3  | B1  | C1  | 

In the table above, A is the key, but C → B.