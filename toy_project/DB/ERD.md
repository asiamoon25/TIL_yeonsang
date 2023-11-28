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
-- auto-generated definition  
create table comment  
(  
    id         bigint auto_increment  
        primary key,    content_no bigint       null,  
    content    text         null,  
    author     varchar(100) null,  
    user_tag   varchar(100) null,  
    constraint comment_FK  
        foreign key (content_no) references board_article (id)  
);
```

reply_comment
```sql
-- auto-generated definition  
create table reply_comment  
(  
    id           bigint auto_increment  
        primary key,    comment_id   bigint       null,  
    content      text         null,  
    reply_author varchar(100) null,  
    user_tag     varchar(100) null,  
    constraint reply_comment_FK  
        foreign key (comment_id) references comment (id)  
);
```