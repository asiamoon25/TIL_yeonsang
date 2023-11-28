![[Pasted image 20231129001243.png]]

query
board_type
```sql
-- auto-generated definition  
create table board_tytpe  
(  
    type_name varchar(100) null,  
    type_code varchar(100) null,  
    id        bigint auto_increment  
        primary key);

```
board_article
```sql
-- auto-generated definition  
create table board_article  
(  
    title         varchar(100) null,  
    content       varchar(100) null,  
    views         int          null,  
    board_type_id bigint       null,  
    id            bigint auto_increment  
        primary key,    constraint board_article_FK  
        foreign key (board_type_id) references board_tytpe (id)  
);
```

comment
```sql

```
