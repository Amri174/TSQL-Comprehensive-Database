## PLSQL


### PLSQL BLOCK

**Simple Variable Declaration and Assignment:**
````
declare
  a1 number(5);
  b number(5);
begin
  a1:=5;
  b:=a1*4;
  dbms_output.put_line('Value: '||b);
end;
/
````
**With constants:**
````
declare
  a1 constant number(4):=11;
  b constant number(4):=6;
begin
  dbms_output.put_line('Value: '||a1);
end;
/
````
**Input Substitution and Arithmetic:**
````
declare
  a1 number(4);
  b1 number(4);
  c1 number(4);
begin
  a1:=&a1;
  b1:=&b1;
  c1:= a1+b1;
  dbms_output.put_line('Sum: '||c1);
end;
/
````
**Conditional Statements:**

````
declare
  n Varchar2(20);
begin
  update demo set name='Hussain' where id=48;
  if sql%found then
    n:='updated';
  elsif sql%notfound then
    n:='unupdated';
  end if;
  dbms_output.put_line(n);
end;
/
````


### STORED PROCEDURE

**Procedure Creation and Execution:**

````
create or replace procedure grey(msg in Varchar) is
begin
  dbms_output.put_line('Grey Matter '||msg);
end;
/
exec grey('is GM');
````
````
create or replace procedure
hello(stock in Varchar,rise in integer,fall in integer) is
begin
  dbms_output.put_line('Stock'||'Rise'||'Fall');
  dbms_output.put_line(stock||' '||rise||' '||fall);
end;
/
exec hello('Japan Candle',821,134);
````
**Arithmetic:**
````
declare
  a number(3);
  b number(3);
  c number(3);
  procedure product(a in number,b in number,c out number) is
  begin
    c:=a*b;
    dbms_output.put_line('Product: '||c);
  end;
begin
  a:=3;
  b:=5;
  product(a,b,c);
end;
/
````
**Procedures with IN and OUT Parameters**
````
create or replace procedure p1(idd in number,name1 out Varchar) as
begin
  select name into name1 from demo where id=idd;
end;
/
declare
  idd number(10);
  name1 Varchar(20);
begin
  idd:=15;
  p1(idd, name1);
  dbms_output.put_line('End');
end;
/
````
**Procedures with Exception Handling**
````
create or replace procedure p1(
  idd    in  number,
  name1  out varchar
) as
begin
  select name into name1 from demo where id = idd;
exception
  when no_data_found then
    name1 := 'No such ID';
  when others then
    name1 := 'Error: ' || sqlerrm;
end;
/
````


### FUNCTIONS

**Creation and Use:**
````
create or replace function adder(n in number)
return Varchar2 as
  a Varchar2(10);
begin
  hello(n,a);
  return a;
end;
/
select adder(48) from dual;
````
````
create or replace function addn(n1 in number)
return number is
  n2 number(10);
begin
  n2 := n1+10;
  return n2;
end;
/
select addn(15) from dual;
````


### CURSORS

**Explicit Cursor with Loop:**
````
declare
  cursor c1(n number) is select * from demo where id<n;
  rr demo%rowtype;
  n number(10);
begin
  n:= &n;
  open c1(n);
  loop
    fetch c1 into rr;
    exit when c1%notfound;
    dbms_output.put_line('Found'||rr.name);
  end loop;
  close c1;
end;
/
````
**Cursor with Parameter:**
````
declare
  cursor c(name1 varchar2) is select * from demo where name=name1;
  rr demo%rowtype;
  n1 varchar2(20);
begin
  n1:= &n1;
  open c(n1);
  loop
    fetch c into rr;
    exit when c%notfound;
    dbms_output.put_line(rr.name);
  end loop;
  close c;
end;
/
````


