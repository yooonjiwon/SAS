# [SAS] Import file

- Import Excel File

```sas
proc import file="C:\Users\data.xlsx" out=dt dbms=xlsx; 
sheet="Sheet 1"; 
run;
```
