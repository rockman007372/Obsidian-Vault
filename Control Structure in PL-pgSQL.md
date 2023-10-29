
In general, SQL functions/procedures can be complex, having variables and control structures. However, SQL does not support these operations. Hence, we must use `LANGUAGE plpgsql` instead.

>[!question]
> Write a function to sort the students in descending order of their Marks. **For each student, compute the difference between his/her mark and the previous student.** 

![[Pasted image 20230311183002.png]]

## Loops

We can loop through the query results with a `for` loop.

```sql
CREATE FUNCTION compute_points_gaps() 
RETURNS TABLE(name TEXT, points INT, gap INT) AS $$ 

DECLARE 
	s RECORD; 
	prev INT; 

BEGIN 
	prev := -1; 
	
	FOR s IN (SELECT * FROM students ORDER BY points DESC) 
	LOOP 
		name := s.name; 
		points := s.points; 
		
		IF prev >= 0 THEN 
			gap := prev - s.points; 
		ELSE 
			gap := 0; 
		END IF; 
		
		RETURN NEXT; 
		prev := s.points; 
	END LOOP; 
END; 

$$ LANGUAGE plpgsql;
```

## Cursors

To go through each tuple in the sorted sequence, we can also use a [[Cursor]].

```sql
CREATE OR REPLACE FUNCTION score_gap() 
RETURNS TABLE(name TEXT, mark INT, gap INT) AS $$
DECLARE 
	curs CURSOR FOR (SELECT * FROM scores ORDER BY mark DESC);
	record RECORD; -- tuple
	previousMark INT;

BEGIN 
	previousMark := -1;
	OPEN curs;
	LOOP
		FETCH curs INTO record;
		EXIT WHEN NOT FOUND;
		score_gap.name := record.Name;
		score_gap.mark := record.Mark;
		IF previousMark == -1 THEN
			gap := NULL;
		ELSE 
			gap := previousMark - Mark;
		END IF;
		RETURN NEXT; -- Insert tuple into the Table output
		previousMark := mark;
	END LOOP;
	CLOSE curs;
END;
$$ LANGUAGE plpgqsl;
```

>[!question]
> Write a function that retrieves the student(s) with the median mark(s).
> For n students, 
> - If n is odd, median is (n + 1)/ 2
> - If n is even, median is n / 2 and (n / 2) + 1  

```sql
CREATE OR REPLACE FUNCTION median_stu()
RETURNS TABLE(name TEXT, mark INT) AS $$
DECLARE
  curs CURSOR FOR (SELECT * FROM Scores ORDER BY Mark DESC);
  r RECORD;
  n INT;
BEGIN
  OPEN curs;
  SELECT COUNT(*) INTO n FROM Scores; -- assign n as row number
  IF n % 2 = 1 THEN
	  FETCH ABSOLUTE (n+1)/2 FROM curs INTO r;
	  name := r.name;
	  mark := r.Mark;
	  RETURN NEXT;
  ELSE
	  FETCH ABSOLUTE n/2 FROM curs INTO r;
	  name := r.name;
	  mark := r.Mark;
	  RETURN NEXT;
	  
	  FETCH ABSOLUTE n/2 + 1 FROM curs INTO r;
	  name := r.name;
	  mark := r.Mark;
	  RETURN NEXT; 
  END IF;
  CLOSE curs;
END;
$$ LANGUAGE plpgsql;
```

Instead of doing 2 `FETCH ABSOLUTE`, we can do one `FETCH ABSOLUTE`, followed by `FETCH NEXT` or `FETCH RELATIVE 1`:

```SQL
FETCH ABSOLUTE n/2 FROM curs INTO r;

-- any of these are equivalent
FETCH ABSOLUTE n/2 + 1 FROM curs INTO r;
FETCT NEXT FROM curs INTO r;
FETCH RELATIVE 1 FROM curs INTO r;
```



