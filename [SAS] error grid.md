# [SAS] Error Grid

This code is alteration of [Jesse A. Canchola's code](https://www.lexjansen.com/wuss/2013/78_Paper.pdf)
Also, alteration is based on Morey et al.

```sas
proc import 
file="data.xlsx"
out=err
dbms=xlsx;
sheet='gdl';
run;

* "Using SAS for Error Grid Analysis (EGA) of Glycated Hemoglobin A1c" ;
* WUSS 2014 - Planet Hollywood, Las Vegas, NV ;
* November 13 to 15, 2013 ;

%let name=hemoglobin_error_grid ;
filename odsout '.' ;
%let dataclr=cx4da5f7 ;
%let grayclr=gray33 ;

* set up the html hover-text for the red plot marker ;
data err ; set err ;
length hover_text $100 ;
hover_text='title='||quote(
'B (g/dL) = '||trim(left(B))||'0d'x||
'A (g/dL) = '||trim(left(A))
 )||
' href="hemoglobin_error_grid_info.htm"' ;
run ;

* set up each colored grid section ;
data anno_colored_areas ;
length function color style $8 ;
xsys='2' ; ysys='2' ;
hsys='3' ; when='b' ;
color='black' ; size=.1 ;
* green area ;
color="#B6D7A8" ; style='solid' ;
function='poly' ;
x=4.0 ; y=4.0 ; output ;
function='polycont' ;
x=6.0 ; y=4.0 ; output ;
x=6.0 ; y=5.4 ; output ;
x=10.0; y=9.0 ; output ;
x=16.0 ; y=9.0 ; output ;
x=16.0 ; y=16.0 ; output ;
x=9.0 ; y=16.0 ; output ;
x=9.0 ; y=10.0 ; output ;
x=5.4 ; y=6.0 ; output ;
x=4.0 ; y=6.0 ; output ;
x=4.0 ; y=4.0 ; output ;
* bottom yellow area ;
color="#FFE599" ; style='solid' ;
function='poly' ;
x=6.0 ; y=4.0 ; output ;
function='polycont' ;
x=6.0 ; y=5.4 ; output ;
x=10.0 ; y=9.0 ; output ;
x=16.0 ; y=9.0 ; output ;
x=16.0 ; y=6.0 ; output ;
x=10.0 ; y=6.0 ; output ;
x=10.0 ; y=4.0 ; output ;
x=6.0 ; y=4.0 ; output ;
* top yellow area ;
color="#FFE599" ; style='solid' ;
function='poly' ;
x=4.0 ; y=6.0 ; output ;
function='polycont' ;
x=5.4 ; y=6.0 ; output ;
x=9.0 ; y=10.0 ; output ;
x=9.0 ; y=16.0 ; output ;
x=6.0 ; y=16.0 ; output ;
x=6.0 ; y=10.0 ; output ;
x=4.0 ; y=10.0 ; output ;
x=4.0 ; y=6.0 ; output ;
* top red area ;
color="#E06666" ; style='solid' ;
function='poly' ;
x=4.0 ; y=10.0 ; output ;
function='polycont' ;
x=4.0 ; y=16.0 ; output ;
x=6.0 ; y=16.0 ; output ;
x=6.0 ; y=10.0 ; output ;
x=4.0 ; y=10.0 ; output ;
* bottom red area ;
color="#E06666" ; style='solid' ;
function='poly' ;
x=10.0 ; y=4.0 ; output ;
function='polycont' ;
x=10.0 ; y=6.0 ; output ;
x=16.0 ; y=6.0 ; output ;
x=16.0 ; y=4.0 ; output ;
x=10.0 ; y=4.0 ; output ;
run ;

data anno_outline ; set anno_colored_areas ;
style='empty' ; color="&grayclr" ;
run ;

data anno_diagonal ;
length function color $8 ;
xsys='2' ; ysys='2' ;
hsys='3' ; when='b' ;
color="black" ; size=.1 ;
function='move' ; x=4.0 ; y=4.0 ; output ;
function='draw' ; x=16.0 ; y=16.0 ; line=33 ; output ;
run ;

data anno_letters ;
length function color $8 ;
xsys='2' ; ysys='2' ;
hsys='3' ; when='b' ;
color="&grayclr" ; size=. ;
function='label' ; position='5' ;
text='A' ; x=10.0 ; y=15.5 ; output ;
text='B' ; x=7.0 ; y=13.0 ; output ;
text='A' ; x=14.0 ; y=10.0 ; output ;
text='B' ; x=11.0 ; y=8.0 ; output ;
text='C' ; x=13.0 ; y=5.0 ; output ;
text='C' ; x=5.0 ; y=13.0 ; output ;
run ;

data anno_all ; set anno_colored_areas anno_outline anno_diagonal
anno_letters ;
run ;
goptions device=png ypixels=725 xpixels=700 ;
goptions noborder ;
ods listing close ;

ods html path=odsout body="&name..htm"
 (title="Error Grid for A vs. B (g/dL)")
style=sasweb ;
goptions gunit=pct htitle=3.5 ftitle="times new roman/bold" htext=2.5
ftext="times new roman/bold" ;
axis1 order=(4.0 to 16.0 by 2) minor=(number=1) offset=(0,0) length=5.0in
label=(angle=90) ;
axis2 order=(4.0 to 16.0 by 2) minor=(number=1) offset=(0,0) length=5.0in
label=(angle=0) ;
symbol1 value=dot height=2.5 interpol=rl width=2 color="#83B1DA"
ci="#83B1DA" ;
* draw a smooth circle around the blue dot * ;
symbol2 value=circle height=2.5 interpol=none color=&grayclr ;
title1 " " ;

proc gplot data=err anno=anno_all ;
plot B*A=1 B*A=2 / overlay
vaxis=axis1 haxis=axis2 noframe
html=hover_text
des='' name="&name" ;
footnote1 "Error Grid for A vs. B (g/dL)" ;
run ;
quit ;

ods html close ;
ods listing ;

run;
