# [SAS] Wide to Long

```python
proc transpose data=dt_wide out=dt_long;
by id;
var var1-var2;
run;
```
