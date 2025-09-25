---
Note_Type: Daily
cssclasses:
  - cards
---
## BrainDump


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