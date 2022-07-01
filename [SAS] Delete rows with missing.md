# [SAS] Delete rows with missing.md
   
```sas
data changed;
set original;
if cmiss(of _all_) then delete;
run;
```
