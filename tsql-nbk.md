-- create tableone
create table dbo.tableone (
    id int primary key identity(1,1),
    name varchar(50),
    is_active bit
);

-- create tabletwo
create table dbo.tabletwo (
    id int primary key identity(1,1),
    tableone_id int,
    amount decimal(10,2),
    foreign key (tableone_id) references dbo.tableone(id)
);

-- insert sample data into tableone
insert into dbo.tableone (name, is_active) values
('alice', 1),
('bob', 1),
('charlie', 0),
('david', 1);

-- insert sample data into tabletwo
insert into dbo.tabletwo (tableone_id, amount) values
(1, 100.50),
(1, 200.00),
(2, 300.75);

-- view joined result
select t1.id, t1.name, t1.is_active, t2.amount
from dbo.tableone as t1
left join dbo.tabletwo as t2
    on t1.id = t2.tableone_id
order by t1.id;
