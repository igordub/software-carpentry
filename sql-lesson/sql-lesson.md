```sql
(base) igordub@home:~/github/software-carpentry/sql-lesson$ sqlite3 survey.db 
SQLite version 3.32.3 2020-06-18 14:00:33
Enter ".help" for usage hints.
sqlite> .tables
Person   Site     Survey   Visited
sqlite> .schema
CREATE TABLE Person (id text, personal text, family text);
CREATE TABLE Site (name text, lat real, long real);
CREATE TABLE Survey (taken integer, person text, quant text, reading real);
CREATE TABLE Visited (id integer, site text, dated text);
sqlite> SELECT family, personal FROM Person
   ...> 
Dyer|William
Pabodie|Frank
Lake|Anderson
Roerich|Valentina
Danforth|Frank
(base) igordub@home:~/github/software-carpentry/sql-lesson$ sqlite3 survey.db 
SQLite version 3.32.3 2020-06-18 14:00:33
Enter ".help" for usage hints.
sqlite> SELECT family, personal FROM Person;
Dyer|William
Pabodie|Frank
Lake|Anderson
Roerich|Valentina
Danforth|Frank
sqlite> SELECT family, personal FROM Person
   ...> ;
Dyer|William
Pabodie|Frank
Lake|Anderson
Roerich|Valentina
Danforth|Frank
sqlite> .mode column
sqlite> .header on
sqlite> SELECT family, personal FROM Person;
family      personal  
----------  ----------
Dyer        William   
Pabodie     Frank     
Lake        Anderson  
Roerich     Valentina 
Danforth    Frank     
sqlite> SELECT * FROM Person;
id          personal    family    
----------  ----------  ----------
dyer        William     Dyer      
pb          Frank       Pabodie   
lake        Anderson    Lake      
roe         Valentina   Roerich   
danforth    Frank       Danforth  
sqlite> SELECT personal, family FROM Person;
personal    family    
----------  ----------
William     Dyer      
Frank       Pabodie   
Anderson    Lake      
Valentina   Roerich   
Frank       Danforth  
sqlite> .schema
CREATE TABLE Person (id text, personal text, family text);
CREATE TABLE Site (name text, lat real, long real);
CREATE TABLE Survey (taken integer, person text, quant text, reading real);
CREATE TABLE Visited (id integer, site text, dated text);
sqlite> SELECT name FROM Site;
name      
----------
DR-1      
DR-3      
MSK-4     
sqlite> SELECT quant FROM Survey;
quant     
----------
rad       
sal       
rad       
sal       
rad       
sal       
temp      
rad       
sal       
temp      
rad       
temp      
sal       
rad       
sal       
temp      
sal       
rad       
sal       
sal       
rad       
sqlite> SELECT DISTINCT quant FROM Survey ;
quant     
----------
rad       
sal       
temp      
sqlite> SELECT taken, quant FROM Survey ;
taken       quant     
----------  ----------
619         rad       
619         sal       
622         rad       
622         sal       
734         rad       
734         sal       
734         temp      
735         rad       
735         sal       
735         temp      
751         rad       
751         temp      
751         sal       
752         rad       
752         sal       
752         temp      
752         sal       
837         rad       
837         sal       
837         sal       
844         rad       
sqlite> SELECT * FROM Person;
id          personal    family    
----------  ----------  ----------
dyer        William     Dyer      
pb          Frank       Pabodie   
lake        Anderson    Lake      
roe         Valentina   Roerich   
danforth    Frank       Danforth  
sqlite> SELECT * FROM Person ORDER BY id;
id          personal    family    
----------  ----------  ----------
danforth    Frank       Danforth  
dyer        William     Dyer      
lake        Anderson    Lake      
pb          Frank       Pabodie   
roe         Valentina   Roerich   
sqlite> SELECT * FROM Person ORDER BY family;
id          personal    family    
----------  ----------  ----------
danforth    Frank       Danforth  
dyer        William     Dyer      
lake        Anderson    Lake      
pb          Frank       Pabodie   
roe         Valentina   Roerich   
sqlite> SELECT * FROM Person ORDER BY personal;
id          personal    family    
----------  ----------  ----------
lake        Anderson    Lake      
pb          Frank       Pabodie   
danforth    Frank       Danforth  
roe         Valentina   Roerich   
dyer        William     Dyer      
sqlite> SELECT * FROM Person ORDER BY id, personal;
id          personal    family    
----------  ----------  ----------
danforth    Frank       Danforth  
dyer        William     Dyer      
lake        Anderson    Lake      
pb          Frank       Pabodie   
roe         Valentina   Roerich   
sqlite> SELECT personal, family  FROM Person ORDER BY personal, family ;
personal    family    
----------  ----------
Anderson    Lake      
Frank       Danforth  
Frank       Pabodie   
Valentina   Roerich   
William     Dyer      
sqlite> SELECT personal, family  FROM Person ORDER BY personal, DESC  ;
Error: no such column: DESC
sqlite> SELECT personal, family  FROM Person ORDER BY personal DESC  ;
personal    family    
----------  ----------
William     Dyer      
Valentina   Roerich   
Frank       Pabodie   
Frank       Danforth  
Anderson    Lake      
sqlite> SELECT personal, family  FROM Person ORDER BY personal ASC;
personal    family    
----------  ----------
Anderson    Lake      
Frank       Pabodie   
Frank       Danforth  
Valentina   Roerich   
William     Dyer      
sqlite> .schema
CREATE TABLE Person (id text, personal text, family text);
CREATE TABLE Site (name text, lat real, long real);
CREATE TABLE Survey (taken integer, person text, quant text, reading real);
CREATE TABLE Visited (id integer, site text, dated text);
sqlite> SELECT * FROM Visited ;
id          site        dated     
----------  ----------  ----------
619         DR-1        1927-02-08
622         DR-1        1927-02-10
734         DR-3        1930-01-07
735         DR-3        1930-01-12
751         DR-3        1930-02-26
752         DR-3                  
837         MSK-4       1932-01-14
844         DR-1        1932-03-22
sqlite> SELECT dated, 1927-02-08  FROM Visited ;
dated       1927-02-08
----------  ----------
1927-02-08  1917      
1927-02-10  1917      
1930-01-07  1917      
1930-01-12  1917      
1930-02-26  1917      
            1917      
1932-01-14  1917      
1932-03-22  1917      
sqlite> SELECT dated FROM Visited ;
dated     
----------
1927-02-08
1927-02-10
1930-01-07
1930-01-12
1930-02-26
          
1932-01-14
1932-03-22
sqlite> SELECT personal, family FROM Person ORDER BY family;
personal    family    
----------  ----------
Frank       Danforth  
William     Dyer      
Anderson    Lake      
Frank       Pabodie   
Valentina   Roerich   
sqlite> SELECT DISTINCT dated FROM Visited ;
dated     
----------
1927-02-08
1927-02-10
1930-01-07
1930-01-12
1930-02-26
          
1932-01-14
1932-03-22
sqlite> SELECT * FROM Visited ;
id          site        dated     
----------  ----------  ----------
619         DR-1        1927-02-08
622         DR-1        1927-02-10
734         DR-3        1930-01-07
735         DR-3        1930-01-12
751         DR-3        1930-02-26
752         DR-3                  
837         MSK-4       1932-01-14
844         DR-1        1932-03-22
sqlite> SELECT * FROM Visited WHERE site = 'DR-1';
id          site        dated     
----------  ----------  ----------
619         DR-1        1927-02-08
622         DR-1        1927-02-10
844         DR-1        1932-03-22
sqlite> SELECT * FROM Visited WHERE site = 'DR-1' AND dated < '1930-01-01';
id          site        dated     
----------  ----------  ----------
619         DR-1        1927-02-08
622         DR-1        1927-02-10
sqlite> SELECT *
   ...> FROM Visited 
   ...> WHERE Site = 'DR-1' AND dated < '1930-01-01';
id          site        dated     
----------  ----------  ----------
619         DR-1        1927-02-08
622         DR-1        1927-02-10
sqlite> SELECT * FROM Survey WHERE person = 'lake' OR person = 'roe;
   ...> ;
   ...> .quit
   ...> ^D
Error: unrecognized token: "'roe;
;
.quit"
(base) igordub@home:~/github/software-carpentry/sql-lesson$ sqlite3 survey.db 
SQLite version 3.32.3 2020-06-18 14:00:33
Enter ".help" for usage hints.
sqlite> SELECT * FROM Survey WHERE person = 'lake' OR person = 'roe';
734|lake|sal|0.05
751|lake|sal|0.1
752|lake|rad|2.19
752|lake|sal|0.09
752|lake|temp|-16.0
752|roe|sal|41.6
837|lake|rad|1.46
837|lake|sal|0.21
837|roe|sal|22.5
844|roe|rad|11.25
sqlite> .mode column
sqlite> .header on
sqlite> SELECT * FROM Survey WHERE person = 'lake' OR person = 'roe';
taken       person      quant       reading   
----------  ----------  ----------  ----------
734         lake        sal         0.05      
751         lake        sal         0.1       
752         lake        rad         2.19      
752         lake        sal         0.09      
752         lake        temp        -16.0     
752         roe         sal         41.6      
837         lake        rad         1.46      
837         lake        sal         0.21      
837         roe         sal         22.5      
844         roe         rad         11.25     
sqlite> SELECT * FROM Survey WHERE person IN ('lake', 'roe');
taken       person      quant       reading   
----------  ----------  ----------  ----------
734         lake        sal         0.05      
751         lake        sal         0.1       
752         lake        rad         2.19      
752         lake        sal         0.09      
752         lake        temp        -16.0     
752         roe         sal         41.6      
837         lake        rad         1.46      
837         lake        sal         0.21      
837         roe         sal         22.5      
844         roe         rad         11.25     
sqlite> SELECT * FROM Survey WHERE quant = 'sal' AND person='lake' OR person='roe;
   ...> '
   ...> ;
taken       person      quant       reading   
----------  ----------  ----------  ----------
734         lake        sal         0.05      
751         lake        sal         0.1       
752         lake        sal         0.09      
837         lake        sal         0.21      
sqlite> SELECT * FROM Survey WHERE quant = 'sal' AND person='lake' OR person='roe';
taken       person      quant       reading   
----------  ----------  ----------  ----------
734         lake        sal         0.05      
751         lake        sal         0.1       
752         lake        sal         0.09      
752         roe         sal         41.6      
837         lake        sal         0.21      
837         roe         sal         22.5      
844         roe         rad         11.25     
sqlite> SELECT * FROM Survey WHERE quant = 'sal' AND (person='lake' OR person='roe');
taken       person      quant       reading   
----------  ----------  ----------  ----------
734         lake        sal         0.05      
751         lake        sal         0.1       
752         lake        sal         0.09      
752         roe         sal         41.6      
837         lake        sal         0.21      
837         roe         sal         22.5      
sqlite> SELECT * FROM Survey WHERE quant = 'sal' AND (person IN ('lake','roe'));
taken       person      quant       reading   
----------  ----------  ----------  ----------
734         lake        sal         0.05      
751         lake        sal         0.1       
752         lake        sal         0.09      
752         roe         sal         41.6      
837         lake        sal         0.21      
837         roe         sal         22.5      
sqlite> SELECT * FROM Visited ;
id          site        dated     
----------  ----------  ----------
619         DR-1        1927-02-08
622         DR-1        1927-02-10
734         DR-3        1930-01-07
735         DR-3        1930-01-12
751         DR-3        1930-02-26
752         DR-3                  
837         MSK-4       1932-01-14
844         DR-1        1932-03-22
sqlite> SELECT * FROM Visited WHERE site LIKE 'DR%';
id          site        dated     
----------  ----------  ----------
619         DR-1        1927-02-08
622         DR-1        1927-02-10
734         DR-3        1930-01-07
735         DR-3        1930-01-12
751         DR-3        1930-02-26
752         DR-3                  
844         DR-1        1932-03-22
sqlite> SELECT * FROM Visited WHERE site LIKE 'M%';
id          site        dated     
----------  ----------  ----------
837         MSK-4       1932-01-14
sqlite> SELECT DISTINCT person, quant FROM Survey WHERE person='lake' OR person='roe';
person      quant     
----------  ----------
lake        sal       
lake        rad       
lake        temp      
roe         sal       
roe         rad       
sqlite> SELECT person, quant FROM Survey ;
person      quant     
----------  ----------
dyer        rad       
dyer        sal       
dyer        rad       
dyer        sal       
pb          rad       
lake        sal       
pb          temp      
pb          rad       
            sal       
            temp      
pb          rad       
pb          temp      
lake        sal       
lake        rad       
lake        sal       
lake        temp      
roe         sal       
lake        rad       
lake        sal       
roe         sal       
roe         rad       
sqlite> SELECT person, quant FROM Survey WHERE person IN ('lake', 'roe');
person      quant     
----------  ----------
lake        sal       
lake        sal       
lake        rad       
lake        sal       
lake        temp      
roe         sal       
lake        rad       
lake        sal       
roe         sal       
roe         rad       
sqlite> SELECT DIST person, quant FROM Survey WHERE person IN ('lake', 'roe');
Error: no such column: DIST
sqlite> SELECT DISTINCT  person, quant FROM Survey WHERE person IN ('lake', 'roe');
person      quant     
----------  ----------
lake        sal       
lake        rad       
lake        temp      
roe         sal       
roe         rad       
sqlite> SELECT DISTINCT  person, quant FROM Survey;
person      quant     
----------  ----------
dyer        rad       
dyer        sal       
pb          rad       
lake        sal       
pb          temp      
            sal       
            temp      
lake        rad       
lake        temp      
roe         sal       
roe         rad       
sqlite> SELECT * FROM Site WHERE (lat > -48) OR (lat < 48);
name        lat         long      
----------  ----------  ----------
DR-1        -49.85      -128.57   
DR-3        -47.15      -126.72   
MSK-4       -48.87      -123.4    
sqlite> SELECT * FROM Site WHERE (lat > -48) AND (lat < 48);
name        lat         long      
----------  ----------  ----------
DR-3        -47.15      -126.72   
sqlite> SELECT * FROM Survey;
taken       person      quant       reading   
----------  ----------  ----------  ----------
619         dyer        rad         9.82      
619         dyer        sal         0.13      
622         dyer        rad         7.8       
622         dyer        sal         0.09      
734         pb          rad         8.41      
734         lake        sal         0.05      
734         pb          temp        -21.5     
735         pb          rad         7.22      
735                     sal         0.06      
735                     temp        -26.0     
751         pb          rad         4.35      
751         pb          temp        -18.5     
751         lake        sal         0.1       
752         lake        rad         2.19      
752         lake        sal         0.09      
752         lake        temp        -16.0     
752         roe         sal         41.6      
837         lake        rad         1.46      
837         lake        sal         0.21      
837         roe         sal         22.5      
844         roe         rad         11.25     
sqlite> SELECT * FROM Survey WHERE quant='sal';
taken       person      quant       reading   
----------  ----------  ----------  ----------
619         dyer        sal         0.13      
622         dyer        sal         0.09      
734         lake        sal         0.05      
735                     sal         0.06      
751         lake        sal         0.1       
752         lake        sal         0.09      
752         roe         sal         41.6      
837         lake        sal         0.21      
837         roe         sal         22.5      
sqlite> SELECT * FROM Survey WHERE quant='sal' AND (reading > 1.00 OR reading < 0.0);
taken       person      quant       reading   
----------  ----------  ----------  ----------
752         roe         sal         41.6      
837         roe         sal         22.5      
sqlite> SELECT reading FROM Survey WHERE quant = 'rad';
reading   
----------
9.82      
7.8       
8.41      
7.22      
4.35      
2.19      
1.46      
11.25     
sqlite> SELECT 1.05 * reading FROM Survey WHERE quant = 'rad';
1.05 * reading
--------------
10.311        
8.19          
8.8305        
7.581         
4.5675        
2.2995        
1.533         
11.8125       
sqlite> SELECT taken, reading FROM Survey WHERE quant = 'temp';
taken       reading   
----------  ----------
734         -21.5     
735         -26.0     
751         -18.5     
752         -16.0     
sqlite> SELECT taken, round(5*(reading-32)/9, 2) FROM Survey WHERE quant = 'temp';
taken       round(5*(reading-32)/9, 2)
----------  --------------------------
734         -29.72                    
735         -32.22                    
751         -28.06                    
752         -26.67                    
sqlite> SELECT taken, round(5*(reading-32)/9, 2) AS celsius FROM Survey WHERE quant = 'temp';
taken       celsius   
----------  ----------
734         -29.72    
735         -32.22    
751         -28.06    
752         -26.67    
sqlite> SELECT personal || ' ' || family FROM Person;
personal || ' ' || family
-------------------------
William Dyer             
Frank Pabodie            
Anderson Lake            
Valentina Roerich        
Frank Danforth           
sqlite> SELECT personal || ' ' || family AS full name FROM Person;
Error: near "name": syntax error
sqlite> SELECT personal || ' ' || family AS full_name FROM Person;
full_name   
------------
William Dyer
Frank Pabodi
Anderson Lak
Valentina Ro
Frank Danfor
sqlite> SELECT * FROM Person WHERE id = 'dyer';
id          personal    family    
----------  ----------  ----------
dyer        William     Dyer      
sqlite> SELECT * FROM Person WHERE id = 'roe';
id          personal    family    
----------  ----------  ----------
roe         Valentina   Roerich   
sqlite> SELECT * FROM Person WHERE id = 'dyer' UNION SELECT * FROM Person WHERE id = 'roe';
id          personal    family    
----------  ----------  ----------
dyer        William     Dyer      
roe         Valentina   Roerich   
sqlite> SELECT * FROM Person WHERE id IN ('dyer', 'roe'));
Error: near ")": syntax error
sqlite> SELECT * FROM Person WHERE id IN ('dyer', 'roe');
id          personal    family    
----------  ----------  ----------
dyer        William     Dyer      
roe         Valentina   Roerich   
sqlite> SELECT * FROM Survey WHERE quant='sal';
taken       person      quant       reading   
----------  ----------  ----------  ----------
619         dyer        sal         0.13      
622         dyer        sal         0.09      
734         lake        sal         0.05      
735                     sal         0.06      
751         lake        sal         0.1       
752         lake        sal         0.09      
752         roe         sal         41.6      
837         lake        sal         0.21      
837         roe         sal         22.5      
sqlite> SELECT * FROM Survey WHERE quant='sal' AND person = 'roe';
taken       person      quant       reading   
----------  ----------  ----------  ----------
752         roe         sal         41.6      
837         roe         sal         22.5      
sqlite> SELECT *, reading / 100  FROM Survey WHERE quant='sal' AND person = 'roe';
taken       person      quant       reading     reading / 100
----------  ----------  ----------  ----------  -------------
752         roe         sal         41.6        0.416        
837         roe         sal         22.5        0.225        
sqlite> SELECT  reading / 100 FROM Survey WHERE quant='sal' AND person = 'roe';
reading / 100
-------------
0.416        
0.225        
sqlite> SELECT taken='752' reading / 100 FROM Survey WHERE quant='sal' AND person = 'roe' UNION SELECT taken='619' reading / 100 FROM Survey WHERE quant='sal' AND person = 'roe';
Error: near "/": syntax error
sqlite> SELECT taken='752', reading / 100 FROM Survey WHERE quant='sal' AND person = 'roe' UNION SELECT taken='619', reading / 100 FROM Survey WHERE quant='sal' AND person = 'roe';
taken='752'  reading / 100
-----------  -------------
0            0.225        
0            0.416        
1            0.416        
sqlite> SELECT * FROM Visited ;
id          site        dated     
----------  ----------  ----------
619         DR-1        1927-02-08
622         DR-1        1927-02-10
734         DR-3        1930-01-07
735         DR-3        1930-01-12
751         DR-3        1930-02-26
752         DR-3                  
837         MSK-4       1932-01-14
844         DR-1        1932-03-22
sqlite> .nullvalue -null-
sqlite> SELECT * FROM Visited ;
id          site        dated     
----------  ----------  ----------
619         DR-1        1927-02-08
622         DR-1        1927-02-10
734         DR-3        1930-01-07
735         DR-3        1930-01-12
751         DR-3        1930-02-26
752         DR-3        -null-    
837         MSK-4       1932-01-14
844         DR-1        1932-03-22
sqlite> SELECT * FROM Visited WHERE dated = NULL;
sqlite> SELECT * FROM Visited WHERE dated IS NULL;
id          site        dated     
----------  ----------  ----------
752         DR-3        -null-    
sqlite> SELECT * FROM Visited WHERE dated NOT NULL;
id          site        dated     
----------  ----------  ----------
619         DR-1        1927-02-08
622         DR-1        1927-02-10
734         DR-3        1930-01-07
735         DR-3        1930-01-12
751         DR-3        1930-02-26
837         MSK-4       1932-01-14
844         DR-1        1932-03-22
sqlite> SELECT * FROM Survey WHERE quant = 'sal' AND person != 'lake';
taken       person      quant       reading   
----------  ----------  ----------  ----------
619         dyer        sal         0.13      
622         dyer        sal         0.09      
752         roe         sal         41.6      
837         roe         sal         22.5      
sqlite> SELECT * FROM Survey WHERE quant = 'sal' AND (person != 'lake' or person IS NULL);
taken       person      quant       reading   
----------  ----------  ----------  ----------
619         dyer        sal         0.13      
622         dyer        sal         0.09      
735         -null-      sal         0.06      
752         roe         sal         41.6      
837         roe         sal         22.5      
sqlite> SELECT * FROM Visited ;
id          site        dated     
----------  ----------  ----------
619         DR-1        1927-02-08
622         DR-1        1927-02-10
734         DR-3        1930-01-07
735         DR-3        1930-01-12
751         DR-3        1930-02-26
752         DR-3        -null-    
837         MSK-4       1932-01-14
844         DR-1        1932-03-22
sqlite> SELECT * FROM Visited ORDER BY dated ;
id          site        dated     
----------  ----------  ----------
752         DR-3        -null-    
619         DR-1        1927-02-08
622         DR-1        1927-02-10
734         DR-3        1930-01-07
735         DR-3        1930-01-12
751         DR-3        1930-02-26
837         MSK-4       1932-01-14
844         DR-1        1932-03-22
sqlite> SELECT * FROM Visited ORDER BY dated WHERE dated NOT NULL;
Error: near "WHERE": syntax error
sqlite> SELECT * FROM Visited WHERE dated NOT NULL ORDER BY dated ;
id          site        dated     
----------  ----------  ----------
619         DR-1        1927-02-08
622         DR-1        1927-02-10
734         DR-3        1930-01-07
735         DR-3        1930-01-12
751         DR-3        1930-02-26
837         MSK-4       1932-01-14
844         DR-1        1932-03-22
sqlite> SELECT * FROM Visited WHERE dated IN ('1927-02-08', NULL);
id          site        dated     
----------  ----------  ----------
619         DR-1        1927-02-08
sqlite> SELECT * FROM Visited WHERE (dated AND dated IS NULL) IN ('1927-02-08', NULL);
sqlite> SELECT * FROM Visited WHERE (dated OR dated IS NULL) IN ('1927-02-08', NULL);
sqlite> SELECT * FROM Visited WHERE (dated OR dated IS NULL);
id          site        dated     
----------  ----------  ----------
619         DR-1        1927-02-08
622         DR-1        1927-02-10
734         DR-3        1930-01-07
735         DR-3        1930-01-12
751         DR-3        1930-02-26
752         DR-3        -null-    
837         MSK-4       1932-01-14
844         DR-1        1932-03-22
sqlite> SELECT * FROM Visited WHERE (dated OR dated IS NULL) IN ('1927-02-08', NULL);
sqlite> SELECT dated FROM Visited ;
dated     
----------
1927-02-08
1927-02-10
1930-01-07
1930-01-12
1930-02-26
-null-    
1932-01-14
1932-03-22
sqlite> SELECT count( dated) FROM Visited ;
count( dated)
-------------
7            
sqlite> SELECT count(dated) FROM Visited ;
count(dated)
------------
7           
sqlite> #
sqlite> # NULL is ommited in arithmetic expressions
sqlite> SELECT avg(reading) FROM Survey WHERE quant = 'sal';;
avg(reading)    
----------------
7.20333333333333
sqlite> SELECT sum(reading) FROM Survey WHERE quant = 'sal';;
sum(reading)
------------
64.83       
sqlite> SELECT max(reading) FROM Survey WHERE quant = 'sal';;
max(reading)
------------
41.6        
sqlite> SELECT min(reading) FROM Survey WHERE quant = 'sal';;
min(reading)
------------
0.05        
sqlite> SELECT count(*) FROM Survey ;
count(*)  
----------
21        
sqlite> SELECT * FROM Survey ;
taken       person      quant       reading   
----------  ----------  ----------  ----------
619         dyer        rad         9.82      
619         dyer        sal         0.13      
622         dyer        rad         7.8       
622         dyer        sal         0.09      
734         pb          rad         8.41      
734         lake        sal         0.05      
734         pb          temp        -21.5     
735         pb          rad         7.22      
735         -null-      sal         0.06      
735         -null-      temp        -26.0     
751         pb          rad         4.35      
751         pb          temp        -18.5     
751         lake        sal         0.1       
752         lake        rad         2.19      
752         lake        sal         0.09      
752         lake        temp        -16.0     
752         roe         sal         41.6      
837         lake        rad         1.46      
837         lake        sal         0.21      
837         roe         sal         22.5      
844         roe         rad         11.25     
sqlite> SELECT person, count(reading), avg(reading)
   ...> FROM Survey 
   ...> WHERE quant = 'rad'
   ...> GROUP BY person;
person      count(reading)  avg(reading)
----------  --------------  ------------
dyer        2               8.81        
lake        2               1.825       
pb          3               6.66        
roe         1               11.25       
sqlite> SELECT person, count(reading), avg(reading)
   ...> FROM Survey
   ...> WHERE quant = 'rad';
person      count(reading)  avg(reading)
----------  --------------  ------------
dyer        8               6.5625      
sqlite> SELECT person, quant, count(reading), avg(reading)
   ...> FROM Survey
   ...> GROUP BY person, quant;
person      quant       count(reading)  avg(reading)
----------  ----------  --------------  ------------
-null-      sal         1               0.06        
-null-      temp        1               -26.0       
dyer        rad         2               8.81        
dyer        sal         2               0.11        
lake        rad         2               1.825       
lake        sal         4               0.1125      
lake        temp        1               -16.0       
pb          rad         3               6.66        
pb          temp        2               -20.0       
roe         rad         1               11.25       
roe         sal         2               32.05       
sqlite> SELECT * FROM Survey ;
taken       person      quant       reading   
----------  ----------  ----------  ----------
619         dyer        rad         9.82      
619         dyer        sal         0.13      
622         dyer        rad         7.8       
622         dyer        sal         0.09      
734         pb          rad         8.41      
734         lake        sal         0.05      
734         pb          temp        -21.5     
735         pb          rad         7.22      
735         -null-      sal         0.06      
735         -null-      temp        -26.0     
751         pb          rad         4.35      
751         pb          temp        -18.5     
751         lake        sal         0.1       
752         lake        rad         2.19      
752         lake        sal         0.09      
752         lake        temp        -16.0     
752         roe         sal         41.6      
837         lake        rad         1.46      
837         lake        sal         0.21      
837         roe         sal         22.5      
844         roe         rad         11.25     
sqlite> SELECT * FROM Person;
id          personal    family    
----------  ----------  ----------
dyer        William     Dyer      
pb          Frank       Pabodie   
lake        Anderson    Lake      
roe         Valentina   Roerich   
danforth    Frank       Danforth  
sqlite> SELECT * FROM Survey JOIN PErson;
taken       person      quant       reading     id          personal    family    
----------  ----------  ----------  ----------  ----------  ----------  ----------
619         dyer        rad         9.82        dyer        William     Dyer      
619         dyer        rad         9.82        pb          Frank       Pabodie   
619         dyer        rad         9.82        lake        Anderson    Lake      
619         dyer        rad         9.82        roe         Valentina   Roerich   
619         dyer        rad         9.82        danforth    Frank       Danforth  
619         dyer        sal         0.13        dyer        William     Dyer      
619         dyer        sal         0.13        pb          Frank       Pabodie   
619         dyer        sal         0.13        lake        Anderson    Lake      
619         dyer        sal         0.13        roe         Valentina   Roerich   
619         dyer        sal         0.13        danforth    Frank       Danforth  
622         dyer        rad         7.8         dyer        William     Dyer      
622         dyer        rad         7.8         pb          Frank       Pabodie   
622         dyer        rad         7.8         lake        Anderson    Lake      
622         dyer        rad         7.8         roe         Valentina   Roerich   
622         dyer        rad         7.8         danforth    Frank       Danforth  
622         dyer        sal         0.09        dyer        William     Dyer      
622         dyer        sal         0.09        pb          Frank       Pabodie   
622         dyer        sal         0.09        lake        Anderson    Lake      
622         dyer        sal         0.09        roe         Valentina   Roerich   
622         dyer        sal         0.09        danforth    Frank       Danforth  
734         pb          rad         8.41        dyer        William     Dyer      
734         pb          rad         8.41        pb          Frank       Pabodie   
734         pb          rad         8.41        lake        Anderson    Lake      
734         pb          rad         8.41        roe         Valentina   Roerich   
734         pb          rad         8.41        danforth    Frank       Danforth  
734         lake        sal         0.05        dyer        William     Dyer      
734         lake        sal         0.05        pb          Frank       Pabodie   
734         lake        sal         0.05        lake        Anderson    Lake      
734         lake        sal         0.05        roe         Valentina   Roerich   
734         lake        sal         0.05        danforth    Frank       Danforth  
734         pb          temp        -21.5       dyer        William     Dyer      
734         pb          temp        -21.5       pb          Frank       Pabodie   
734         pb          temp        -21.5       lake        Anderson    Lake      
734         pb          temp        -21.5       roe         Valentina   Roerich   
734         pb          temp        -21.5       danforth    Frank       Danforth  
735         pb          rad         7.22        dyer        William     Dyer      
735         pb          rad         7.22        pb          Frank       Pabodie   
735         pb          rad         7.22        lake        Anderson    Lake      
735         pb          rad         7.22        roe         Valentina   Roerich   
735         pb          rad         7.22        danforth    Frank       Danforth  
735         -null-      sal         0.06        dyer        William     Dyer      
735         -null-      sal         0.06        pb          Frank       Pabodie   
735         -null-      sal         0.06        lake        Anderson    Lake      
735         -null-      sal         0.06        roe         Valentina   Roerich   
735         -null-      sal         0.06        danforth    Frank       Danforth  
735         -null-      temp        -26.0       dyer        William     Dyer      
735         -null-      temp        -26.0       pb          Frank       Pabodie   
735         -null-      temp        -26.0       lake        Anderson    Lake      
735         -null-      temp        -26.0       roe         Valentina   Roerich   
735         -null-      temp        -26.0       danforth    Frank       Danforth  
751         pb          rad         4.35        dyer        William     Dyer      
751         pb          rad         4.35        pb          Frank       Pabodie   
751         pb          rad         4.35        lake        Anderson    Lake      
751         pb          rad         4.35        roe         Valentina   Roerich   
751         pb          rad         4.35        danforth    Frank       Danforth  
751         pb          temp        -18.5       dyer        William     Dyer      
751         pb          temp        -18.5       pb          Frank       Pabodie   
751         pb          temp        -18.5       lake        Anderson    Lake      
751         pb          temp        -18.5       roe         Valentina   Roerich   
751         pb          temp        -18.5       danforth    Frank       Danforth  
751         lake        sal         0.1         dyer        William     Dyer      
751         lake        sal         0.1         pb          Frank       Pabodie   
751         lake        sal         0.1         lake        Anderson    Lake      
751         lake        sal         0.1         roe         Valentina   Roerich   
751         lake        sal         0.1         danforth    Frank       Danforth  
752         lake        rad         2.19        dyer        William     Dyer      
752         lake        rad         2.19        pb          Frank       Pabodie   
752         lake        rad         2.19        lake        Anderson    Lake      
752         lake        rad         2.19        roe         Valentina   Roerich   
752         lake        rad         2.19        danforth    Frank       Danforth  
752         lake        sal         0.09        dyer        William     Dyer      
752         lake        sal         0.09        pb          Frank       Pabodie   
752         lake        sal         0.09        lake        Anderson    Lake      
752         lake        sal         0.09        roe         Valentina   Roerich   
752         lake        sal         0.09        danforth    Frank       Danforth  
752         lake        temp        -16.0       dyer        William     Dyer      
752         lake        temp        -16.0       pb          Frank       Pabodie   
752         lake        temp        -16.0       lake        Anderson    Lake      
752         lake        temp        -16.0       roe         Valentina   Roerich   
752         lake        temp        -16.0       danforth    Frank       Danforth  
752         roe         sal         41.6        dyer        William     Dyer      
752         roe         sal         41.6        pb          Frank       Pabodie   
752         roe         sal         41.6        lake        Anderson    Lake      
752         roe         sal         41.6        roe         Valentina   Roerich   
752         roe         sal         41.6        danforth    Frank       Danforth  
837         lake        rad         1.46        dyer        William     Dyer      
837         lake        rad         1.46        pb          Frank       Pabodie   
837         lake        rad         1.46        lake        Anderson    Lake      
837         lake        rad         1.46        roe         Valentina   Roerich   
837         lake        rad         1.46        danforth    Frank       Danforth  
837         lake        sal         0.21        dyer        William     Dyer      
837         lake        sal         0.21        pb          Frank       Pabodie   
837         lake        sal         0.21        lake        Anderson    Lake      
837         lake        sal         0.21        roe         Valentina   Roerich   
837         lake        sal         0.21        danforth    Frank       Danforth  
837         roe         sal         22.5        dyer        William     Dyer      
837         roe         sal         22.5        pb          Frank       Pabodie   
837         roe         sal         22.5        lake        Anderson    Lake      
837         roe         sal         22.5        roe         Valentina   Roerich   
837         roe         sal         22.5        danforth    Frank       Danforth  
844         roe         rad         11.25       dyer        William     Dyer      
844         roe         rad         11.25       pb          Frank       Pabodie   
844         roe         rad         11.25       lake        Anderson    Lake      
844         roe         rad         11.25       roe         Valentina   Roerich   
844         roe         rad         11.25       danforth    Frank       Danforth  
sqlite> SELECT * FROM Survey JOIN Person ON Survey.person = Person.id;
taken       person      quant       reading     id          personal    family    
----------  ----------  ----------  ----------  ----------  ----------  ----------
619         dyer        rad         9.82        dyer        William     Dyer      
619         dyer        sal         0.13        dyer        William     Dyer      
622         dyer        rad         7.8         dyer        William     Dyer      
622         dyer        sal         0.09        dyer        William     Dyer      
734         pb          rad         8.41        pb          Frank       Pabodie   
734         lake        sal         0.05        lake        Anderson    Lake      
734         pb          temp        -21.5       pb          Frank       Pabodie   
735         pb          rad         7.22        pb          Frank       Pabodie   
751         pb          rad         4.35        pb          Frank       Pabodie   
751         pb          temp        -18.5       pb          Frank       Pabodie   
751         lake        sal         0.1         lake        Anderson    Lake      
752         lake        rad         2.19        lake        Anderson    Lake      
752         lake        sal         0.09        lake        Anderson    Lake      
752         lake        temp        -16.0       lake        Anderson    Lake      
752         roe         sal         41.6        roe         Valentina   Roerich   
837         lake        rad         1.46        lake        Anderson    Lake      
837         lake        sal         0.21        lake        Anderson    Lake      
837         roe         sal         22.5        roe         Valentina   Roerich   
844         roe         rad         11.25       roe         Valentina   Roerich   
sqlite> SELECT (* AND !id) FROM Survey JOIN Person ON Survey.person = Person.id;
Error: near "*": syntax error
sqlite> SELECT taken, quant, reading, personal, family FROM Survey JOIN Person ON Survey.person = Person.id;
taken       quant       reading     personal    family    
----------  ----------  ----------  ----------  ----------
619         rad         9.82        William     Dyer      
619         sal         0.13        William     Dyer      
622         rad         7.8         William     Dyer      
622         sal         0.09        William     Dyer      
734         rad         8.41        Frank       Pabodie   
734         sal         0.05        Anderson    Lake      
734         temp        -21.5       Frank       Pabodie   
735         rad         7.22        Frank       Pabodie   
751         rad         4.35        Frank       Pabodie   
751         temp        -18.5       Frank       Pabodie   
751         sal         0.1         Anderson    Lake      
752         rad         2.19        Anderson    Lake      
752         sal         0.09        Anderson    Lake      
752         temp        -16.0       Anderson    Lake      
752         sal         41.6        Valentina   Roerich   
837         rad         1.46        Anderson    Lake      
837         sal         0.21        Anderson    Lake      
837         sal         22.5        Valentina   Roerich   
844         rad         11.25       Valentina   Roerich  
```