# Assignment: Triggers

# Set A:

**Question a**

```plpgsql
--Trigger
create or replace trigger callback update on item_sup before update for each
row execute beforeUpdate();

--Function

create or replace function beforeUpdate() returns trigger as $$

begin

if (NEW.rate - OLD.rate)>2000 or (OLD.rate - NEW.rate)>2000 then
raise exception 'Difference is greater than 2000';

end if;
end;
$$
language 'plpgsql';
```

**Question b**

```plpgsql
--Trigger
create or replace trigger callinsert on item_sup before insert or update for each
row execute before();

--Function

create or replace function before() returns trigger as $$

begin

if NEW.rate <> 0 then
raise exception 'Rate cannot be zero';
end if;
end;
$$
language 'plpgsql';
```
***

## Set B:

**Question a**

```plpgsql
--Trigger
create or replace trigger calldelete on student before delete for each
row execute beforeDelete();

--Function

create or replace function beforeDelete() returns trigger as $$

begin

raise notice 'Student record is being deleted ';

end;
$$
language 'plpgsql';
```
**Question b**

```plpgsql
--Trigger
create or replace trigger callbinsert on stu_sub before insert or update for each
row execute beforebInsert();

--Function

create or replace function beforebInsert() returns trigger as $$

begin

if NEW.marks<10 or NEW.marks>100 then
 raise exception 'Invalid marks entered';
end if;

end;
$$
language 'plpgsql';
```
***
#### Set C:

**Question a**

```plpgsql
--Trigger
create or replace trigger inter_insert on cities before insert for each row execute oninsert();

--Function

create or replace function oninsert() returns trigger as $$

begin

if length (NEW.pincode) > 6 or length (NEW.pincode) < 6 then
raise exception 'Pincode must be 6 character';
end;
$$
language 'plpgsql';
```

**Question b**

```plpgsql
--Trigger
create or replace trigger inter_delete on cities before delete for each row execute ondelete();

--Function

create or replace function ondelete() returns trigger as $$

begin

if OLD.state <> 'Maharashtra' then
raise exception 'Can't delete cities from Maharashtra';
end if;

end;
$$
language 'plpgsql';
```

