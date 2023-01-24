---
tags: university
aliases: 
---
Date:: 2022-08-05 Friday
Links: 
- - -
# Dataview and Templaters for School
### Dataview Commands

```dataview
TABLE year AS Year, semester AS Semester
FROM #course AND "Assignments" OR [[Computer Science]]
WHERE year = "1" AND semester = "1" AND !"Excalidraw"
````

### Process-later Note System
- We can create notes with tags 'toProcess" for lecture notes and create concept notes later!
- Especially useful during lectures
- Create dataview for "toProcess" in the main note