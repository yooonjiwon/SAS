# [SAS] Inner join
   
```python
data merged;
merge first (IN=in_no_first) second (IN=in_no_second);
by id;
run;
```
