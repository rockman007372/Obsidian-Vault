
>[!definition]
> A key is a [[superkey]] that is also **minimal**.

- Minimal = cannot be made smaller
- If (A, B, C) is a key then (A, B) cannot be a superkey

>[!Properties]
> -   If _(A, B, C)_ is _definitely_ a **_superkey_** then _(A, B, C, D)_ is a **_superkey_** 
> -   If _(A, B)_ is _definitely_ a **_superkey_** then _(A, B, C)_ is **NOT** a **_key_** → _(A, B, C)_ is not minimal!
> -   If _(A, B)_ is _definitely_ a **_key_** then _it is possible that_ _(B, C)_ is also a **_key_**  
> -   Every relations have at least 1 superkey 

**Example:**

Consider a forum database with the following relation filled with many thousands of users: _Accounts(userId: **INT**, email: **TEXT**, password: **TEXT**, name: **TEXT**)_.

Using reasonable guess, which subsets of attributes are **superkeys** of relation _Accounts_?

**Answer:**

{userID} = key = superkey
~~{password} = key~~  *you should never make password key*
{email, password} = superkey 

Using a userID, you can uniquely identify the email and password associated with it.