# Survival Analysis

## Kaplan Meier
```sas
proc lifetest method=km plot=(s ls lls) graphics;
time days*status(0);
strata group; /*in case you want to compare two groups.*/
run;
```

## Nelson-Alen Estimate
```sas
proc lifetest method=km nelson plot=(s ls lls) graphics outsurv=df2;
time days*status(0);
run;
```
