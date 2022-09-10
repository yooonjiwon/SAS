# Survival Analysis

## Kaplan Meier
```sas
proc lifetest method=km plot=(s ls lls) graphics;
time time*status(0);
run;
```

## Nelson-Alen Estimate
```sas
proc lifetest method=km nelson plot=(s ls lls) graphics outsurv=df2;
time time*status(0);
run;
```
