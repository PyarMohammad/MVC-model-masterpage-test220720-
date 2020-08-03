create database mvcmodel22720
use mvcmodel22720

--alter database mvccontroller22720m1 modify name =  mvccontroller22720

--alter table Student add status int default 0

--alter table Student add inserted_date date

--alter table Student add course varchar(50)

-------------------------------------------------------------------

create table tblStudent
(
  id int primary key identity,
  name varchar(50),
  age int,
  ctr int,
  str int,
  gender varchar(50),
  dob varchar(50),
  inserted_date varchar(50),
  status int default 0,
  email varchar(50),
  pwd varchar(50),
  cnf_pwd varchar(50),
)

select *from tblStudent
-------------------------------------------------------------------------------

create table tblCountry
(
cid int primary key identity,
cname varchar(50)
)
insert into tblCountry(cname)values('IND'),('PAK'),('BEG')

select * from tblCountry

------------------------------------------------------------------------

create table tblState
(
sid int primary key identity,
cid int,
sname varchar(50)
)

insert into tblState(cid,sname)values(1,'UP'),(1,'Bihar'),(2,'Lahor'),(2,'Islamabad'),(3,'Vuhan'),(3,'Hong Kong')

select * from tblState
------------------------------------------------------------------------

alter proc usp_tblStudent
@action varchar(50)=null,
@id int=0,
@name varchar(50)=null,
@age int=0,
@ctr int=0,
@str int=0,
@gender varchar(50)=null,
@dob varchar(50)=null,
@email varchar(50)=null,
@pwd varchar(50)=null,
@cnf_pwd varchar(50)=null
as
begin
       if(@action='insert')
	   begin
	         insert into tblStudent(name,age,ctr,str,gender,dob,inserted_date,email,pwd,cnf_pwd)values(@name,@age,@ctr,@str,@gender,@dob,GETDATE(),@email,@pwd,@cnf_pwd)
	   end


      else if(@action='bindcon')
	  begin
	  select *from tblCountry
	  end

	  else if(@action='bindstate')
	  begin
	  select *from tblState where cid=@id
	  end

      else if(@action='show')
	  begin
	  select *from tblStudent where status=0
	  end

      else if(@action='delete')
	  begin
	  update tblStudent set status=1 where id=@id
	  end

      else if(@action='edit')
	  begin
	  select *from tblStudent where id=@id
	  end

      else if(@action='update')
	  begin
	  update tblStudent set name=@name, age=@age, ctr=@ctr, str=@str, gender=@gender, dob=@dob, email=@email, pwd=@pwd, cnf_pwd=@cnf_pwd where id=@id 
	  end

      else if(@action='join')
	  begin
	  select *, CONVERT(varchar(50), inserted_date, 106)idate from tblStudent
	   inner join tblCountry on tblStudent.ctr=cid
	   inner join tblState on tblStudent.str=sid
	   where status=0
	  end
end

select * from tblStudent
select * from tblCountry
select * from tblState




truncate table  tblStudent