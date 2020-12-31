# JSP-blog-project

## 환경 
- WINDOWS
- JDK 1.8
- tomcat 9.0
- STS tool
- MySQL 8.0
- postman
- lombok
- Gson (Json 파싱)
- git
- 인코딩 UTF-8

## MySQL 데이터베이스 생성 및 사용자 생성

```sql
create user 'bloguser'@'%' identified by 'bitc5600';
GRANT ALL privileges ON *.* TO 'bloguser'@'%';
create database blog;
use blog;
```

## MySQL 테이블 생성

- bloguser 사용자로 접속
- use blog; 데이터 베이스 선택

```sql
CREATE TABLE user(
    id int primary key auto_increment,
    username varchar(100) not null unique,
    password varchar(100) not null,
    email varchar(100) not null,
    address varchar(100),
    userRole varchar(20),
    createDate timestamp
) engine=InnoDB default charset=utf8;

CREATE TABLE board(
    id int primary key auto_increment,
    userId int,
    title varchar(100) not null,
    content longtext,
    readCount int default 0,
    createDate timestamp,
    foreign key (userId) references users (id)
) engine=InnoDB default charset=utf8;

CREATE TABLE reply(
    id int primary key auto_increment,
    userId int,
    boardId int,
    content varchar(300) not null,
    createDate timestamp,
    foreign key (userId) references users (id) on delete set null,
    foreign key (boardId) references board (id) on delete cascade
) engine=InnoDB default charset=utf8;
```
