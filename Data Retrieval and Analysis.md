## DATA RETRIEVAL AND ANALYSIS

### Filtering Queries

| OPERATOR | QUERY |
|-|-|
| WHERE | select * from laptop where screensize=(select screensize from laptop where model_no='LP114');|
| AND/OR | select * from pc where (ram=128 or ram=256) and hd>=50;|
| IN | select * from trial where id in (20,40);|
| NOT IN | select * from printer where model_no not in('PR112','PR124');|
| BETWEEN | select * from trial where id between 20 and 50; |
| LIKE | select * from product_info where model_no like 'PC%';|
| !=/<> | select * from laptop where screensize!=17;|
| HAVING | select hd,count(*) from pc group by hd having count(hd)>2;|
| ORDER BY | select * from deep order by id desc;|
| Subquery | select * from printer where price= (select price from printer where model_no in(select model_no from product_info where maker='lBM'));|



### Set Operator Queries

````
select name from worker union select name from workerskill;
select name from worker union all select name from workerskill;
select name from worker intersect select name from workerskill;
select name from worker minus select name from workerskill;
````



### Join Operator Queries

````
select * from Product_Info, PC;
select * from Laptop, Printer;
select * from pc, printer;
select * from pc, laptop, printer;

select I.model_no, l.type, p.model_no, p.color 
from Product_Info I, Printer p 
where I.model_no = p.model_no(+);

select I.model_no, l.type, p.model_no, p.color 
from Product_Info I, Printer p 
where I.model_no(+) = p.model_no;

select a.name, a.age, b.skill 
from worker a, workerskill b 
where a.name = b.name(+);

select a.name, a.age, b.skill 
from worker a, workerskill b 
where a.name(+) = b.name;

select w.name, w.age, ws.skill 
from worker w left outer join workerskill ws on w.name = ws.name;
select w.name, w.age, ws.skill 
from worker w right outer join workerskill ws on w.name = ws.name;

select a.maker, b.model_no, b.price 
from product_info a, pc b 
where a.model_no = b.model_no;

select a.name, a.age, b.skill 
from worker a, workerskill b 
where a.age > 30 and a.name = b.name;

select b.name, a.age, b.skill 
from worker a, workerskill b 
where a.age > 35 and a.name <> b.name;
````



### Combining both Set and Join Operator Queries

````
select l.model_no, l.type, p.model_no, p.color 
from Product_Info I, Printer p 
where l.model_no(+)=p.model_no
union
select l.model_no, l.type, p.model_no, p.color 
from Product_Info l, Printer p 
where l.model_no=p.model_no(+);

select p.maker, p.model_no, l.model_no, l.speed 
from Product_Info p, Laptop I 
where p.model_no(+)=l.model_no
union
select p.maker, p.model_no, l.model_no, l.speed 
from Product_Info p, Laptop I 
where p.model_no=l.model_no(+);

select a.name, a.age, b.skill 
from worker a, workerskill b 
where a.name=b.name(+)
union
select a.name, a.age, b.skill 
from worker a, workerskill b 
where a.name=b.name(+);
````


### Aggregate Functions

| AGGREGATE FUNCTION | QUERY |
|--------------------|-------|
| MAX                | select max(id) from demo; |
| MIN                | select min(id) from demo; |
| AVG                | select avg(id) from demo; |
| COUNT              | select count(id) from demo; |
| SUM                | select sum(id) from demo; |
| MAX, MIN, DIFF     | select max(price), min(price), max(price)-min(price) as diff from laptop; |
| STDDEV             | select STDDEV(price), VARIANCE(price) from pc; |
| COUNT + GROUP BY   | select ram, count(*) as PCs from pc group by ram; |
| COUNT + GROUP BY, HAVING | select hd, count(*) as PCs from pc group by hd having count(hd)>2; |

### View/Index

````
create view price_info as
select a.model_no, a.maker, b.price
from product_info a, pc b
where a.model_no = b.model_no and type = 'PC';

create view price20000 as
select * from printer
where price > 20000;

create unique index sno on worker(name);

create index f1 on workerskill(upper(city));
````


### Common Table Expressions (CTEs)

````
create table client_master(
  client_no varchar2(6) primary key,
  name varchar2(20) not null,
  address1 varchar2(30),
  address2 varchar2(30),
  city varchar2(15),
  state varchar2(15),
  pincode number(6),
  bal_due number(10,2)
);

desc client_master;

with temporaryTable(averageValue) as
(select avg(bal_due) from client_master)
select pincode, bal_due
from client_master, temporaryTable
where client_master.bal_due > temporaryTable.averageValue;
````







