# [SAS] Descriptive statistics of continuous variables
```python
proc mean max_dec=3 data=db;
var age;
class group;
run;
```
