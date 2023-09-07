Week ?
---
### Goals Tracker
- [ ] 

### Habit Tracker

```dataview
TABLE WITHOUT ID
  file.link as Date,
  choice(sleep > 6, "✅", "❌") as Sleep,
  choice(breakfast > 0, "✅", "❌") as Breakfast,
  choice(study >= 3, "✅", "❌") as Study,
  choice(pull-ups >= 10, "✅", "❌") as Pull-ups,
  choice(basketball-practice >= 0, "✅", "❌") as Basketball
  
FROM "Daily" AND [[{{title}}]]
SORT file.day ASC
```

### Academic Tracker


### Social Tracker

