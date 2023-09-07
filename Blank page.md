
>[!definition]
> Weak entity sets:
> - do not have its own primary key and
> - must depend on another entity set for identification.


```sql
CREATE TABLE LOAN (
	Loan_no INT PRIMARY KEY,
	Amount NUMERIC,
	Type TEXT,
	Code INT NOT NULL,
	Branch_no INT NOT NULL,
	FOREIGN KEY (Code, Branch_no) REFERENCES BANK_BRANCH(Code, Branch_no)
);
```