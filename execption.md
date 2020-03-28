# Assignment : Exception Handling

## SET A:

**Question a**

```plpgsql
create or replace function disptotale(b_name text) returns int as $$
declare
count_cus int;
begin
 perform * from branch where brname=b_name;

if not found then
raise exception 'Invalid branch name';
end if;

select into count_cus count (*) from customer 
where brname=b_name;

return count_cus;

end;
$$
language 'plpgsql';


```

**Question b**

```plpgsql
create or replace function increLoan() returns void as $$
declare
result cursor for select * from loan_app;
begin

for data in result loop

if data.lmtapproved<10000 then
raise notice 'Loan approved amount is less than 10000';
end if;

end loop;

end;

```
***
### Set B:

**Question a**

```plpgsql
create or replace function dispempe(pro_name text) returns int as $$
declare
count_emp int;
result cursor for select * from emp where eno in(select eno from pro_emp where pno=(select pno from project where pname=pro_name));
begin

perform * from project where pname=pro_name;

if not found then
raise exception 'Invalid project name';
end if;

for data in result loop

raise notice 'employee name=% ',data.ename;

end loop;

select into count_emp count(*) from pro_emp where pno=(select pno from project where pname=pro_name);

return count_emp;

end;
$$
language 'plpgsql';

```

**Question b**

```plpgsql
create or replace function updateEmp() returns void as $$
declare

result cursor for select * from pro_emp;
begin

update pro_emp set no_of_hours_worked=no_of_hours_worked-2;

for data in result loop

if data.no_of_hours_worked<>0 then

raise exception 'no of hours worked is zero ';

end if;
end loop;

end;
$$
language 'plpgsql';

```
***
#### Set C:

**Question a**

```plpgsql
create or replace function ptintn() returns void as $$

declare 
result cursor for select names
from drivers where shift_date='20/04/2014';

begin
for data in result loop
raise notice 'name=%',data;
end loop;
end;
$$
language 'plpgsql';

```

**Question b**

```plpgsql
create or replace function ptintd(int,date) returns void as $$

declare 
result cursor for select *
from drivers where did in(select did from driver_bus where bus_id=$1 and date_shift=$2);

begin

perform  * from bus where bus_id=$1;

if not found then
raise exception 'Enter Valid Bus is';
end if;

for data in result loop
raise notice 'name=%',data.name;
end loop;
end;
$$
language 'plpgsql';

```

