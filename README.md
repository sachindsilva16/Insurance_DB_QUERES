 ### ``` Insurance_DB_QUERES```


> ```create database main_insurance_database;```
> ```use main_insurance_database;```

``` --Person ```
> create table person(
Driver_id varchar(10) primary key,
Fname varchar(30),
Lname varchar(30),
Address varchar(30)
);


```--Car```

> create table car(
Reg_number varchar(10) primary key,
Model varchar(20),
Model_year int
);

```--Accident```

> create table accident(
Report_number varchar(10) primary key,
Accident_date date,
Location varchar(20)
);


```--Owns```

> create table owns(
Driver_id varchar(10),
Reg_number varchar(10)
);


```--Participated```

> create table participated(
Driver_id varchar(10),
Reg_number varchar(10),
Report_number varchar(10),
Damage_amount int
);


```--Foreign Keys```

> alter table owns add foreign key(Driver_id) references person(Driver_id);

> alter table owns add foreign key(Reg_number) references car(Reg_number);

> alter table participated add foreign key(reg_number) references car(Reg_number);

> alter table participated add foreign key(Driver_id) references person(Driver_id);

> alter table participated add foreign key(Report_number) references accident(Report_number);


```--Insert table : Person```

> insert into person values('UDP000192','Rohan','Holt','Udupi');
> insert into person values('MNG001494','Stuart','Olivera','Mangalore');
> insert into person values('UDP008753','Sachin','Rons','Udupi');
> insert into person values('CF096543','John','Smith','California');
> insert into person values('BNG008567','Sohan','Fernandes','Bangalore');
> insert into person values('MMB004563','Steve','Josh','Mumbai');
> insert into person values('UDP004519','Shaun','Paul','Udupi');
> insert into person values('MNG008734','Shawn','Dsouza','Shirva');
> insert into person values('MNG897654','Sanith','Shetty','Mangalore');

--update person set Address='California'
--where Driver_id='CF096543';


```Displaying Database Tables:```

> select * from person;
> select * from car;
> select * from accident;
> select * from owns;
> select * from participated;

```--Insert table : Car```

> insert into car values('KA20M1231','Nissan Altima','2022');
> insert into car values('MH02G1472','Audi A4','2020');
> insert into car values('PB04B332','BMW X7','2022');
> insert into car values('MH24G2671','Porshe 911','2021');
> insert into car values('KA21M4699','Celerio','2019');
> insert into car values('JK14U897','Mercedes A-Class','2021');
> insert into car values('LD17T5643','MS S-Cross','2018');
> insert into car values('KA99MC9999','Audi A4','2013');
> insert into car values('6TRJ244','Audi Q5','2015');


```--Insert into table : Accident```

> insert into accident values('13579246','2006-07-02','Udupi');
> insert into accident values('13578965','2008-05-11','Udupi');
> insert into accident values('83579786','2020-12-30','Mangalore');
> insert into accident values('26779227','2019-03-25','Karkala');
> insert into accident values('53579289','2019-04-15','Malpe');
> insert into accident values('13577841','2016-08-14','Trasi');
> insert into accident values('33803846','2021-09-05','Kundapur');
> insert into accident values('13867627','2015-03-15','Bangalore');
> insert into accident values('29746637','2016-01-26','Kaup');
> insert into accident values('76473623','2020-09-15','Udupi');
> insert into accident values('76413523','2019-06-14','Mangalore');
> insert into accident values('86473343','2021-04-01','California');



```--Insert into table : Owns```

> insert into owns values('BNG008567','PB04B332');
> insert into owns values('MNG008734','LD17T5643');
> insert into owns values('UDP000192','MH02G1472');
> insert into owns values('UDP004519','MH24G2671');
> insert into owns values('MMB004563','KA21M4699');
> insert into owns values('UDP008753','JK14U897');
> insert into owns values('MNG001494','KA20M1231');
> insert into owns values('MNG897654','KA99MC9999');
> insert into owns values('CF096543','6TRJ244');



```--Insert into table : Participated```

> insert into participated values('MNG008734','LD17T5643','29746637',20000);
> insert into participated values('UDP004519','MH24G2671','13867627',100000);
> insert into participated values('UDP008753','JK14U897','33803846',15500);
> insert into participated values('BNG008567','PB04B332','13577841',22000);
> insert into participated values('UDP000192','MH02G1472','345008753',12000);
> insert into participated values('MNG001494','KA20M1231','13579246',33300);
> insert into participated values('MNG897654','KA99MC9999','76413523',1000);
> insert into participated values('CF096543','6TRJ244','86473343',70000);




select * from person;
select * from car;
select * from accident;
select * from owns;
select * from participated;





```--1.Update damage amount of an accident whose report number and car's register number is specified as '135' and 'KA99MC9999' respectively```

> update participated set Damage_amount=2000
where Report_number like '%135%' and Reg_number='KA99MC9999';


--select Report_number,Reg_number,Damage_amount
--from participated
--where Report_number like '%135%' and Reg_number='KA99MC9999';

```--2.Add a new accident into the database```
> insert into accident values('64729173','2021-03-22','Pune');

```--3.Find the # of accidents in which car belonging to 'John Smith' involved```
> select count(*) as No_of_Accidents
from person as p,participated as pa,accident as a
where p.fname='John' and p.Lname='Smith' and a.Report_number=pa.Report_number and p.Driver_id=pa.Driver_id;

```--4.Find the total # of people who owns cars that were involved accidents of the year 2021```

> select count(*) as No_of_People
from accident as ac,owns as o,participated as pa
where ac.Accident_date like '%2021%' and o.Reg_number=pa.Reg_number and pa.Report_number=ac.Report_number;

