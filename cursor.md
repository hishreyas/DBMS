
# Assignmint :Cursor

## Set A:

**Question a**

```plpgsql

craete or replace function getWare(city_w text) returns text as $$
decalre
info text=' ';
result cursor for select * from warehouse where city=city_w;

begin
for data in result loop

info=info||data.wname||E'\n';

end loop;

return info;

end;
$$
language'plpgsql';

```
**Question b**

```plpgsql

craete or replace function getItems() returns text as $$
decalre
info text=' ';

result cursor for select * from items where cost between 500.00 and 800.00;

begin
for data in result loop

info=info||data.itemno||' '||data.description||E'\n';

end loop;

return info;

end;
$$
language'plpgsql';

```

### set B

**Question a**

```plpgsql
create or replace function tfShare() returns void as $$

declare

s_cur cursor for select * from per_cus where pname='Sachin';
r_cur cursor for select * from per_cus where pname='Rahul';
temp int:=0;

begin

for data1 in s_cur loop

for data2 in r_cur loop

temp:=data1.no_of_share;

if data1.cname<>data2.cname then

update cur_per set no_of_share=0 where pname=data1.pname and
 cname=data1.cname;

update cur_per set no_of_share=no_of_share +temp where pname=data2.pname and
 cname=data2.cname;

end if;

end loop;
end loop;

raise notice "Share Transfered successfully ";

end;

```

**Question b**

```plpgsql
create or replace function dispShare() returns void as $$

declare

p_cur cursor for select * from person;
r_cur cursor(persn text) for select * from per_cus where pname=persn;

temp money;
total money:=0;

begin

for data1 in p_cur loop

total:=0;
for data2 in r_cur(data1.pname) loop

select into temp share_value from company where cname=data2.cname;

total:=total+temp*data2.no_of_share;

end loop;

raise notice "Investor=% total invested value=%",data1.pname,total;

end loop;

raise notice "Share Transfered successfully ";

end;

```



#### Set C:

**Question a**

```plpgsql

create or replace function getDetails(adr text) returns void
as $$
declare
result cursor for select * from student,subject,stu_sub where student.rollno=stu_sub.rollno and
subject.scode=stu_sub.scode and student.address=adr;

begin

for data in result loop

raise notice "name=%  subject=%  marks=%",data.name,data.subject_name,data.marks;

end loop;
end;
$$
language 'plpgsql';

```

**Question b**

```plpgsql

create or replace function getPerc() returns void
as $$
declare
names cursor for select * from student;
info cursor (r int) from select * from stu_sub where rollno=r;
counts int;
marks_ int:=0;

begin 

for data1 in names loop 

count:=0;

for data in info(data1.rollno) loop
count:=count+1;
marks_ = marks_ + data.marks;
end loop;

if counts!=0 then
raise notice "student =% total=% percentage=% ",data1.name,marks_,marks_/count;

end if;

end loop;

end;
$$
language 'plpgsql';

```

