# ASSIGNMENT :STORED FUNCTION

## SET A:

**Question a**

```plpgsql
create or replace function disptotal(b_name text) returns int as $$
declare
count_cus int;
begin

select into count_cus count (*) from customer 
where brname=b_name;

return count_cus;

end;
$$
language 'plpgsql';


```
**Question b**

```plpgsql
create or replace function  dispmax(b_name text) returns money as $$
declare
max_money money;
begin

select into max_money max(lmtapproved) from loan_app;

return max_money;


end;
$$
language 'plpgsql';





```





***








### Set B:



**Question a**

```plpgsql
create or replace function dispemp(pro_name text) returns int as $$
declare
count_emp int;
begin

select into count_emp count(*) from pro_emp where pno=(select pno from project where pname=pro_name);

return count_emp;
end;
$$
language 'plpgsql';


```

**Question b**

```plpgsql
create or replace function demp() returns int as $$
declare
count_emp int;
begin

select into count_emp count(*) from emp where join_date <'03-10-2010' ;

return count_emp;
end;
$$
language 'plpgsql';











```

***

### Set C:

**Question a**


```plpgsql
create or replace function disexp() returns int as $$
declare
trip_info text;
row_data trip%rowtype;
begin

for row_data in select * from trip where tno=(select distinct tno
from expense where amt=(select max(amt) from expense))
loop
  trip_info:=trip_info || row_data.trip_name || ' ';

end loop;


return trip_info;
end;
$$
language 'plpgsql';





```

**Question b**

```plpgsql
create or replace function dispc() returns int as $$
declare
count_trip int;
begin

select into count_trip count(*) from trip where from_city='Pune' and to_city='Mumbai';

return count_trip;
end;
$$
language 'plpgsql';

```



