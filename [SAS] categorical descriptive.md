# [SAS] categorical descriptive

```python
PROC FREQ DATA=dataset;
    TABLES variable(s);
RUN;
```

- Contingency table with chi-square test.

```python
PROC FREQ DATA=dataset;
    TABLES variable1*variable2 / chisq;
RUN;
```
