# [SAS] Merge dataset

## Inner Join
```sas
data merged;
merge first (IN=in_no_first) second (IN=in_no_second);
by id;
run;
```

```sas
proc sort data=df1;
by id;
run;

proc osrt data=df2;
by id;
run;

data combined;
merge df1 df2;
by id;
run;
```
