Week ?
---
### Goals 
- [ ] 

### Weekly Target
- [ ] 


### Habit Tracker

```dataview
TABLE WITHOUT ID
  file.link as Date,
  choice(exercise > 0, "✅", "❌") as Exercise,
  choice(breakfast > 0, "✅", "❌") as Breakfast,
  choice(sleep > 6, "✅", "❌") as Sleep,
  choice(study >= 3, "✅", "❌") as Study,
  choice(reflection > 0, "✅", "❌") as Reflection,
  choice(news > 0, "✅", "❌") as News
FROM "Daily" AND [[{{title}}]]
SORT file.day ASC
```

### Academic


### Social 

