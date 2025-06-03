## DML TABLE MANAGEMENT

### Product_Info Table

````
insert into Product_Info values('Dell','DLLA','PC');
insert into Product_Info values('HPL','HPA','LP');
insert into Product_Info values('&Maker','&Model_No','&Type');

select * from Product_Info;

update Product_Info set Type='PR' where Model_No= 'DL123';
update Product_Info set Model_No='DLL46' where Type = 'PC';
update Product_Info set Maker='IBM' where Model_No='HPA';
update Product_Info set Model_No='IBM40' where Maker ='IBM';
update Product_Info set Model_No ='HP40' where maker = 'IBc';

--price_info is view created from Product_Info Table
update price_info set price=50000 where model_no='PC122';
update pc set price=55000 where model_no='PC112';
````


### PC Table

````
insert into PC(model_no,speed,ram,hd,cd,price) values('PC100',3,256,40,52,50000);

select * from PC;

delete from PC;

insert into PC values('&Model_No',&Speed,&RAM,&HD,&CD,&Price);

update PC set Speed=2;
````


### Laptop Table

````
insert into Laptop values('&Model_No', &Speed, &RAM, &HD, &Screensize, &Price);

select * from Laptop;
````


### Printer Table

````
insert into Printer values('&Model_No','&Color','&Type',&Price);

select * from Printer;

--price20000 is view created from Printer Table
delete from price20000 where model_no='PR134';

SELECT * FROM Printer 
WHERE price > (SELECT AVG(price) FROM Printer);
````

### type_info Table

````
select * from type_info;
````

### WORKERSKILL Table

````
insert into WORKERSKILL values ('&name','&skill','&city',&phone);

select * from WORKERSKILL;

update WORKERSKILL set city='MADURAI' where name='JOHN PEARSON' AND
skill='SMITHY';
update WORKERSKILL set phone='91-0435-33333' where name='HELEN BRANDT' AND
skill='COMBINE DRIVER';
select * from Laptop;
update WORKERSKILL set name='JOHN PEARSON' where skill='COMBINE DRIVER' AND
city='CHENNAI';
update WORKERSKILL set phone='' where name='JOHN PEARSON';

delete from WORKERSKILL;

delete from type_info;
````


### trial Table (not inclusive)

````
insert into trial values(&id);

select * from trial;
select * from trial where id in (20,40);
select * from trial where id=10 or id=30 or id=50;
select * from trial where id between 20 and 50;
select id-5 as newid from trial;
select * from trial order by id desc;
````


## DUAL TABLE

````
desc dual;
select * from dual;

insert int dual values(&dummy);

select length('App') from dual;
select length('Abdul') from dual;
select instr('abdul','d') from dual;
select instr('shah','d') from dual;
select instr('appple','p',-1,2) from dual;
select substr('applet',1,3) from dual;
select substr('jelly',-1,2) from dual;
select lpad('dell',10,'@') from dual;
select rpad('kim',20,'!') from dual;
select ltrim('windblows','w') from dual;
select ltrim('kakazana','ka') from dual;
select replace(dummy,'X','Y') from dual;
select translate('zoommeetimg','om','ew') from dual;

select sysdate from dual;
select to_char(sysdate,'dd-mon-yyyy') as "DATE" from dual;
select to_char(sysdate,' month dd yyyy') as "DATE" from dual;
select to_char(sysdate,'dd-mm-yy hh:mi:ss') as "DATE" from dual;

delete from dual;
````


## METADATA QUERY
````
select table_name,constraint_name,constraint_type from user_constraints;
select constraint_name,constraint_type from user_constraints where table_name= 'Product_Info';
select * from tab;
````


