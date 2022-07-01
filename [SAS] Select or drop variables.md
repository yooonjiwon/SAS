# [SAS] Select or drop variables
   
```sas
data changed;
set original (keep= id age)
run;
```
```sas
data changed;
set original (drop= id age)
run;
```
