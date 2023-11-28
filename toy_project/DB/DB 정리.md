
* DB 설계는 자기가 맡은 업무에 속한 것만 한다.


board_type
board_article
board_group

## board_type
bigint id
varchar type_name
varchar type_code



## board_group
bigint id
varchar board_group_name
varchar board_type_id



## board_article
bigint id
varchar title
varchar board_group_id
varchar keyword
varchar content
int views



## coment
bigint id
bigint content_no
varchar content
varchar comment_author
varchar user_tag

## reply_coment
bigint id
bigint comment_id
varchar content
varhcar reply_author
varchar user_tag