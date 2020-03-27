# Assignment: Triggers

## Set C:

**Question a**

```plpgsql
--Trigger
create or replace trigger inter_insert on cities before insert for each row execute oninsert();

--Function

create or replace function oninsert() returns trigger as $$

begin

if length (NEW.pincode) > 6 or length (NEW.pincode) < 6 then
raise exception "Pincode must be 6 character";
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
raise exception "Can't delete cities from Maharashtra";
end if;

end;
$$
language 'plpgsql';
```

