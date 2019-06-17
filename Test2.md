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