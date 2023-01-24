---
tags: courses
area: 
year: 
semester: 
date: <% tp.file.creation_date("YYYY-MM-DD dddd") %>
---


## To Process
```dataview
TABLE type as Type
FROM (#toProcess) 
WHERE course = "<% tp.file.title %>"
```

## Notes and Ideas
- [[<% tp.file.title %> Outline]]

## Lectures
```dataview
TABLE
WHERE course = "<% tp.file.title %>" AND type = "lecture"
```

## Tutorials
```dataview
TABLE
WHERE course = "<% tp.file.title %>" AND type = "tutorial"
```

## Assignments
```dataview
TABLE
WHERE course = "<% tp.file.title %>" AND type = "assignment"
```

## Extras
### Grade Breakdown
### Tips
### Emails and Resources
### Important Dates
### Classmates