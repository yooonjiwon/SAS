# [SAS] Descriptive statistics of continuous variables
   
```python
# getting just N, mean, SD, Minimum, and Maximum
proc means max_dec=3 data=db;
var age;
class group;
run;
```
  
```python
# getting N, mean, SD, median, Q1, and Q3
proc means max_dec=3 data=db mean stddev median q1 q3;
var age;
class group;
run;
```
