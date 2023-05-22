## Motivation

- No relationship between entity set and **relationship sets**
- Relationship only exists between entity sets (rectangle to diamond and vice versa)

## Solution

Make relationship set into an entity.

![[Pasted image 20230214160622.png]]

Note:
- A student may work on a project. He/she can either use GPUs on the project or not.
- **Aggregate is a rectangle around a diamond**. The rectangle should not touch the diamond.
- When using the aggregate as an entity set, **the line touches the rectangle**.

## Mapping

![[Pasted image 20230214161129.png]]

```sql
CREATE TABLE Uses (
  gid   INT,
  sid   INT,
  pname  VARCHAR(50),
  hours NUMERIC,
  PRIMARY KEY (gid, sid, pname), -- All PKs in the sets involved
  FOREIGN KEY (sid, pname) REFERENCES Works (sid, pname),
  FOREIGN KEY (gid) REFERENCES (gid)
);
```