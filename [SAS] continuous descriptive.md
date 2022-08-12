# [SAS] Descriptive statistics of continuous variables
   
```sas
# getting just N, mean, SD, Minimum, and Maximum
proc means maxdec=3 data=db;
var age;
class group;
run;
```
  
```sas
# getting N, mean, SD, median, Q1, and Q3
proc means maxdec=3 data=db mean stddev median q1 q3;
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

### Paired t-test
Comparing two dependent groups when you want to compare the measurements with different times or conditions.
```sas
proc ttest data=data alpha=.05;
    paired pre*post;
run;
```

### Independent t-test
Comparing two independent groups with a continuous variable when they are normally distributed
```sas
proc ttest data=data alpha=.05;
    var continuous;
    class group;
run;
```

### Mann-Whitney U Test
comparing two groups with a continuous variable when they are not normally distributed as a nonparametric test.
```sas
proc npar1way data=df wilcoxon;
class group;
var continuous;
run;
```

### ANOVA
comparing multiple groups with a continuous variables when they are normally distributed.
```sas
proc anova data=data;
class group;
model continuous=group;
run;
```

### Kruskal-Wallis
comparing multiple groups with a continuous variables when they are not normally distributed as a nonparametric test.
```sas
proc npar1way data=df wilcoxon dscf;
class group;
var continuous;
run;
```
