---
Note: Daily
cssclasses:
  - cards
---
## BrainDump

make a list where the file modified date is the within the first 5 closest to the current date 

## Recent Notes 
```dataview
TABLE WITHOUT ID
file.link AS "Note",
file.mday AS "Last Mod"
FROM -"Daily Notes"
SORT file.mday DESC
LIMIT 6
```
## Projects and Todo's
```dataview
TABLE WITHOUT ID
file.link AS "Projects",
progress AS "Progress",
topic AS "Area of Interest"
WHERE Note = "Project" AND Progress != 100 AND Topic != "Template" 
```