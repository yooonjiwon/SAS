# [SAS] Descriptive statistics of continuous variables
   
```sas
# getting just N, mean, SD, Minimum, and Maximum
proc means max_dec=3 data=db;
var age;
class group;
run;
```
  
```sas
# getting N, mean, SD, median, Q1, and Q3
proc means max_dec=3 data=db mean stddev median q1 q3;
var age;
class group;
run;
```

## statistical test

### normality test
```sas
proc univariate data=pre normal plot;
var a b c;
run;
```

### t-test
```sas
proc ttest data=data alpha=.05;
    paired pre*post;
run;
```

### ANOVA
comparing multiple groups with categorical variables when they are normally distributed.
```sas
proc anova data=data;
class group;
model continuous=group;
run;
```

### Kruskal-Wallis
comparing multiple groups with categorical variables when they are not normally distributed as a nonparametric statistical method.
```sas
proc npar1way data=df;
class group;
var continuous;
run;
```
