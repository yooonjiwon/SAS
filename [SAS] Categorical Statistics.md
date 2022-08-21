# [SAS] Categorical Statistics

Frequency check.
```sas
PROC FREQ DATA=dataset;
    TABLES variable(s);
RUN;
```

### Chi-squared test
Contingency table with chi-square test.   
In case the exspected cell counts under 5 is 25% or more, you can use fisher's test.
```sas
PROC FREQ DATA=df;
    TABLES variable1*variable2 / chisq fisher;
RUN;
```
