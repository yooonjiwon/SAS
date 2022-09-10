# [SAS] Import file

## Import Excel File

```sas
proc import file="C:\Users\data.xlsx" out=dt dbms=xlsx; 
sheet="Sheet 1"; 
run;
```

## Import sas7bdat file

```sas
libname mylib "C:/Users/you/fileplace"
data df;
set mylib.df;
run;
```
