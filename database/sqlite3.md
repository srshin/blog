## sqlite3 기본 명령
* ref: https://docs.google.com/presentation/d/1r2Dpbn59jsjHpyJguRm4KEnXNThjjOGigPxNATXjkwU/edit#slide=id.g45f8471c7e_0_103
### setting관련
```
sqlite> .mode column         
sqlite> .mode insert      cf. sqlite> .mode [ html | tabs | list | line | csv ]
sqlite> .headers on
sqlite> .width 15 20 20
sqlite> .tables
sqlite> .schema [schema-name]
sqlite> select type, name, tbl_name, sql from sqlite_master;
sqlite> .show
sqlite> .nullvalue null
sqlite> .prompt 'sqlite3> '
sqlite3> .dump
sqlite3> .output ./db/students.sql
sqlite3> VACUUM;
sqlite3> .exit
sqlite> .read ./db/students.sql
sqlite> .output stdout
sqlite> .separator ,
```

### table 만들기
```
CREATE TABLE Student (
id integer primary key autoincrement not null,
name text not null default 'aaa',
mobile text null);
```
```
CREATE TABLE Club (
id integer primary key autoincrement not null,
name text not null,
leader integer not null,
constraint fk_club_leader_student foreign key(leader)
references Student(id)
);
```
### insert 
```
INSERT INTO Student VALUES(1,'홍길동','010-029-0938');
INSERT INTO Student VALUES(2,'홍길순','000-3049-3049');
```
### update
```
update Student set name = 'aaa' where id = 1;
```
### delete
```
delete from Student where id = 3;
```
### join
```
select s.*, ifnull(c.name, '맡은 동아리 없음') as 'club_name'
  from Student s left outer join Club c
	             on c.leader = s.id;
```
### create view 
```create view v_club_student AS
   select b.*, s.name as student_name
	  from Student s inner join Club b on b.leader = s.id;
```
### create trigger 
```
create table StudentHistory(name text);
create trigger tr_student_insert
  before insert on student
	begin
		insert into StudentHistory (name) values (NEW.name); 
	end;
insert into Student(name) values('김삼수');
select * from StudentHistory;

```
