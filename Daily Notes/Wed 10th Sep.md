---
Note: Daily
cssclasses:
  - cards
---
## BrainDump

I want to make nvim a bit more code friendly
I think that this includes having an LSP for python, c and the prettier stack 


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