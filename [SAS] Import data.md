# [SAS] Import data

## Import Excel File
There are several options such as 'csv, access, sav' for dbms if you want to import csv, access, spss database.
```sas
proc import file="C:\Users\data.xlsx" out=dt dbms=xlsx replace; 
sheet="Sheet 1"; 
run;
```

## Import sas7bdat file
```sas
libname mylib "C:/Users/you/fileplace"
data df;
set mylib.db;
run;
```

## Manually enter the data
```sas
data df;
input id char $ age;
1 M 3;
2 F 40;
run;
```
