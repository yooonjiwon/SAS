# [SAS] Statistics of continuous variables
   
```sas
/* getting just N, mean, SD, Minimum, and Maximum */
proc means maxdec=3 data=db;
var age;
class group;
run;
```
  
```sas
/* getting N, mean, SD, median, Q1, and Q3 */
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

### One sample t-test
First, try normality test with **univariate** statement (Check Shapiro-Wilk and Kolomogorov-Sminov).   
If those are normally distributed, you can use t-test, otherwise you can use signed test or signed rank test.   
```sas
proc univariate data=df loccount mu0 = 5 normal;
var value;
run;
```

### Rank test/Signed rank test
You can change **sides** option depending on your research question.
```sas
proc ttest data=df sides=2 alpha=0.05 h0=5;
var value;
run;
```

### Correlation
```sas
proc corr data=df;
var a b c;
with a b c;
run;
```

### Linear regression
```sas
proc reg data=df;
model dependent = a b c;
run;
quit;
```
