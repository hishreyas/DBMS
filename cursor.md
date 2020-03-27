
# Assignmint :Cursor

**Set C:**

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

