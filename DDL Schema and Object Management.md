## DDL TABLE MANAGEMENT

### Product_Info Table

````
create table Product_Info(
Maker Varchar2(5),
Model_No Varchar2(10),
Type char(2));

desc Product_Info;

alter table Product_Info modify(
Type Varchar2(2) not null);

create view price_info as select a.model_no,a.maker,b.price from product_info a,pc b where
a.model_no=b.model_no and type = 'PC';
````


### PC Table

````
create table PC(
Model_No Varchar2(10),
Speed number(10),
RAM number(10),
HD number(10),
CD number(10),
Price number(10));

desc PC;
````


### Laptop Table

````
create table Laptop(
Model_No Varchar2(10),
Speed number(10),
RAM number(10),
HD number(10),
Screensize number(5),
Price number(10));

desc Laptop;
````


### Printer Table

````
create table Printer(
Model_No Varchar2(10),
Color Varchar2(10),
Type char(2),
Price number(10));

desc Printer;

create view price20000 as select * from Printer where price>20000;
delete from price20000 where model_no='PR134';
````

### type_info Table

````
create table type_info as select * from product_info;
````

### WORKERSKILL Table

````
create table WORKERSKILL(
name Varchar2(20),
skill Varchar2(20),
city Varchar2(10),
phone Varchar2(20));

desc WORKERSKILL;
````

### trial Table (not inclusive)

````
create table trial(id number(10));

desc trial;
````

### trialn Table (not inclusive)

````
create table trialn(
id number(10));

alter table trialn add constraint pktn primary key(id);
alter table trialn add constraint fkt foreign key(id) references demo(id) on delete cascade;
alter table trialn drop constraint pktn;
alter table demo drop constraint fkt;
alter table trialn drop constraint fkt;
alter table demo add constraint pkdemo primary key(id);
alter table trialn add constraint fktn foreign key(id) references demo(id);
alter table demo drop constraint pkdemo;
alter table trialn drop constraint fktn;
````


## CONSTRAIN MANAGEMENT

````
alter table Product_Info add constraint pipk primary key(Model_No);

alter table PC add constraint pcpk primary key(Model_No);
alter table PC add constraint pcfk foreign key(Model_No) references PC(Model_No);

alter table Laptop add constraint plpk primary key(Model_No);
alter table Laptop add constraint plfk foreign key(Model_No) references Laptop(Model_No);

alter table Printer add constraint pppk primary key(Model_No);
alter table Printer add constraint ppfk foreign key(Model_No) references Printer(Model_No);
````


