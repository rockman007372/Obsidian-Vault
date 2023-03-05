## Three Main Questions To Ask

Whenver translating an ER model to SQL Schema, ask yourself these 3 questions:

1.  Do the key attributes uniquely identify the rest of the attributes?
2.  Are the lower bound constraints satisfied
    -   Can you have 0 participation?
    -   Must you have 1 participation?
3.  Are the upper bound constraints satisfied
    -   Can you have ∞ participation?
    -   Must you have exactly 1 participation? Also called **Key constraint** because we can enforce this by making the **key** attribute of the **entity set** to be the **key** attribute of the **relationship set.**

## Attribute Mappings

| ER                     | Schema                                                                                                  |
| ---------------------- | ------------------------------------------------------------------------------------------------------- |
| Attributes             | Columns of table                                                                                        |
| Key attribute          | Primary key of table                                                                                    |
| Derived attributes     | Should not appear                                                                                       |
| Composite attributes   | Set of single-valued attributes                                                                         |
| Multivaried attributes | Either create fixed numbers of single-valued attributes or create new table with foreign key constraint | 

## Relationship Mappings

### General

Include **all** the PKs of entity sets participating in the relationship.

![[Pasted image 20230214142919.png]]

```SQL
CREATE TABLE R (
  pk_E1   TYPE REFERENCES ...,
  pk_E2   TYPE REFERENCES ...,
    :      :
  pk_En   TYPE REFERENCES ...,
  A1      TYPE,
  A2      TYPE,
    :      :
  Am      TYPE,
  PRIMARY KEY (pkE1, ..., pk_En) 
);
```

### Cardinality
#### Many-to-Many

![[Pasted image 20230214143157.png]]

```sql
CREATE TABLE FlightInstances (
  fnum      INT REFERENCES Flights,
  fdate     DATE,
  aircraft  VARCHAR(10),
  PRIMARY KEY (fnum, fdate)
);

CREATE TABLE Bookings (
  bid   INT PRIMARY KEY
);

CREATE TABLE Includes (
  fdate DATE,
  fnum  INT,
  bid   INT,
  seat  VARCHAR(10),
  FOREIGN KEY (fnum, fdate) REFERENCES FlightInstances,
  FOREIGN KEY (bid) REFERENCES Bookings,
  PRIMARY KEY (fnum, fdate, bid)
);
```


#### Many-to-One

![[Pasted image 20230214143708.png]]

2 approaches:
- Create 2 entity sets and 1 relationship set. Set the primary key of the relationship set to the PK of the "One" entity set.
- Combine the "One" entity set with the relationship set.

```sql
-- Approach 1
CREATE TABLE Users (
  uid   INT PRIMARY KEY,
  uname VARCHAR(100),
  dob   DATE
);
CREATE TABLE Bookings (
  bid   INT PRIMARY KEY,
  bdate DATE
);

CREATE TABLE Makes (
  uid   INT,
  bid   INT,
  FOREIGN KEY (uid) REFERENCES Users (uid),
  FOREIGN KEY (bid) REFERENCES Bookings (bid),
  PRIMARY KEY (bid) -- Many-to-One constraint
);
```

```sql
-- Approach 2
CREATE TABLE Users (
  uid   INT PRIMARY KEY,
  uname VARCHAR(100),
  dob   DATE
);
-- In this approach,
-- we remove "Bookings"
-- and combine with "makes"
-- into one table

CREATE TABLE MakesBookings (
  uid   INT,
  bid   INT,
  bdate DATE,
  FOREIGN KEY (uid) REFERENCES Users (uid),
  -- no more REFERENCES Bookings (bid)
  PRIMARY KEY (bid) -- Many-to-One constraint
);
```

#### One-to-One

![[Pasted image 20230214144230.png]]

3 approaches:
- Apply both primary key constraint and (not null + unique) on relationship set
- Combine relationship set with one of the entity sets. Use **UNIQUE** and FOREIGN KEY to establish One-to-One constraints.
- Combine both entity sets into one. No more foreign key. This is a **partial solution** because one entity cannot exist without the other.

```sql
-- Approach 1

CREATE TABLE Users (...);
CREATE TABLE CreditCards (...);

--- Assume no table is combined
CREATE TABLE OWN (
	uid   INT UNIQUE NOT NULL REFERENCES Users,
	ccnum INT PRIMARY KEY REFERENCES CreditCards
)
```


```SQL
-- Approach 2

-- Assume CreditCards is not combined
CREATE TABLE Users (
  uid   INT PRIMARY KEY,
  uname VARCHAR(100),
  dob   DATE,
  ccnum INT UNIQUE REFERENCES CreditCards (ccnum) -- CAN BE NULL
);

-- Assume Users is not combined
CREATE TABLE CreditCards (
  ccnum INT PRIMARY KEY,
  exp   DATE,
  uid   INT UNIQUE REFERENCES Users (uid)
);
```

```sql
-- Approach 3
CREATE TABLE Users (
  uid   INT PRIMARY KEY, -- We choose uid to be PK
  uname VARCHAR(100),
  dob   DATE,
  ccnum INT UNIQUE, -- credit card cannot exist without user
  exp   DATE
);
```
### Total Participation

We **cannot** enforce total participation **without** cardinality constraint. However, we can do this in certain cases where we can afford to **remove some attributes** from an entity.

![[Pasted image 20230214171531.png]]

```sql
CREATE TABLE Users (
  id    INT PRIMARY KEY,
  name  VARCHAR(200)
);

-- Combine Bookings with Makes
CREATE TABLE Makes (
  id    INT REFERENCES Users,
  bid   INT,
  src   VARCHAR(20),
  dst   VARCHAR(20),
  -- no more bdate
  PRIMARY KEY (id, bid) -- total participation w/out cardinality
);
```

Why this works:
- Uniquely identify:
	- Key (id) of Users can uniquely identify other attributes.
	- **There is no other attributes in Bookings** besides its key attribute.
- Lower Bound:
	- Users can make no booking (do not insert into Makes).
	- Booking must be made by a user as (id, bid) is primary key.
- Upper Bound:
	- Users can make any n bookings and Bookings can be made by any n users.

### Key + Total Participation

![[Pasted image 20230214144830.png]]

Use Combine + Foreign Key + Not NULL

```sql
CREATE TABLE MakesBookings (
  bid   INT,
  bdate DATE,
  uid   INT NOT NULL, -- Ensures total participation
  FOREIGN KEY (uid) REFERENCES Users (uid)
  PRIMARY KEY (bid) -- Ensures cardinality through UNIQUE
);
```




### Weak Entity

![[Pasted image 20230214145823.png]]

Its PK consists of both the partial key and the owner set's key.

```sql
CREATE TABLE Flights (
	fnum INT,
	orig TEXT,
	dest TEXT,
	Primary Key (fnum)
);

-- Combine with Has
CREATE TABLE FlightInstances (
  fnum     INT REFERENCES Flights (fnum)
    ON DELETE CASCADE -- cannot exist without owner set
    ON UPDATE CASCADE,  
  fdate    DATE,
  aircraft VARCHAR(10),
  PRIMARY KEY (fnum, fdate) -- combine PK
);
```

## Guidelines

Determine which are **_data_** and which are **_operations_** and **captures only the data**.

Guidelines for ER Design:
-   An ER diagram should capture as many constraints as possible (from the requirements)
-   An ER diagram must **NOT** impose any constraints that are not required (by the requirements)
-   Attributes should have the same name _if and only if_ they are _semantically equivalent_ (Universal Schema Assumption)