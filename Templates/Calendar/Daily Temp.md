Week: [[{{date:YYYY}}-W{{date:WW}}]]
- - -
>[!quote]
<% tp.web.daily_quote() %>

>[!todo]
>- [ ] 

## Habits

**Sleep**::
**Breakfast**::
**Study**:: 
**Exercise**:: 
**Reflection**:: 
**Pullups**::
**News**::

## Interesting News Today

```dataview
TABLE 
FROM (#news) AND -"Templates"
WHERE CONTAINS(date, "{{date}}") 
```

## LeetCode Questions Done

```dataview
TABLE difficulty AS Difficulty, topics AS Topics, performance AS Performance
FROM (#LeetCode) AND -"Templates"
WHERE contains(date, "{{date}}") 
```

## Notes

```dataview
TABLE
WHERE date = "{{date}}"
```

## Reflection

### 3 noteable things that happened today

### 3 most important thing I learned today

### Who am I grateful for today

### Areas of Improvement