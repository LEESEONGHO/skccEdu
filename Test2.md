## Problem1
```
with avg as (
select t.type
     , avg(t.amount) as avg
from account t
group by t.type
)
select a.id
     , a.type
     , a.status
     , a.amount
     , round(a.amount-b.avg,2) as difference
from account a
     inner join
     avg b
     on a.type = b.type
where 1=1
and a.status="Active"
;
```

## Problem2
```
create database if not exists problem2;

use problem2;

create external table if not exists solution (
id int,
fname string,
lname string,
address string,
city string,
state string,
zip string,
birthday string,
hireday string
)
comment "employee"
row format delimited fields terminated by "\t"
stored as parquet location "/user/hive/warehouse/employee"
```

## Problem3
```
create external table if not exists solution (
id int,
fname string,
lname string,
hphone string
)
comment "problem3"
row format delimited fields terminated by "\t"
stored as orc location "/user/training/problem3/solution"
;

insert into problem3.solution
select a.id
, a.fname
, a.lname
, a.hphone
from problem3.customer a
     inner join
     problem3.account b
     on a.id = b.custid
where 1=1
  and b.amount < 0
;
```

## Problem4
```
create database if not exists problem4;

create external table if not exists employee1 (
cust_id int,
fname string,
lname string,
adress string,
city string,
state string,
zip string
)
COMMENT "employee1"
ROW FORMAT DELIMITED FIELDS TERMINATED BY "\t"
STORED AS TEXTFILE LOCATION "/user/training/problem4/data/employee1/"
;


create external table if not exists employee2 (
cust_id int,
digit string,
fname string,
lname string,
adress string,
city string,
state string,
zip string
)
COMMENT "employee2"
ROW FORMAT DELIMITED FIELDS TERMINATED BY ","
STORED AS TEXTFILE LOCATION "/user/training/problem4/data/employee2/"
;



create external table if not exists solution (
cust_id int,
fname string,
lname string,
adress string,
city string,
state string,
zip string
)
COMMENT "problem4"
ROW FORMAT DELIMITED FIELDS TERMINATED BY "\t"
STORED AS TEXTFILE LOCATION "/user/training/problem4/solution/"
;


insert into solution
select *
from employee1
where 1=1
and state = 'CA'
union all
select cust_id
, fname
, lname
, adress
, city
, state
, zip
from employee2
where 1=1
and state = 'CA'
;
```