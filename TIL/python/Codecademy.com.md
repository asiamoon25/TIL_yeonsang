https://www.codecademy.com/courses/learn-python/lessons/python-syntax/exercises/a-string

여기서 배우는 중


## 문자열

```python
print 'Hello'
print "Hello"
print "Hell" + "o"
print 'Hell' + 'o'

message1 = "String"
message2 = 'String'
```

* 홑따옴표, 쌍따옴표 둘다 쓸 수 있음.
* 길이에 제한이 없음
* 문자열은 변경할 수 없음. 문자열 작업이 수행될 때마다 메모리에 새 문자열이 생성됨.

## Accessing the Characters of a String
문자열 접근하기

```python
myString = "Hello, World!"

var_1 = myString[0]
var_2 = myString[7:]
var_3 = myString[1:4]

print("var_1:" + var_1) -> var_1: H
print("var_2:" + var_2) -> var_2: World!
print("var_3:" + var_3) -> var_3: ell
```
* 배열 처럼 0번째 부터 시작
* : 콜론은 ~ 부터의 의미 -> 1:4 는 1번째 인덱스부터 4번째 인덱스 까지
* 인덱스를 벗어나면 IndexError 를 발생
```python
name = "phillis"
name[8] -> Throws an IndexError
```

### 여러줄의 문자열

* 세개의 쌍따옴표로 시작됨.
```python
my_string = """If it were done when 'tis done, then 'twere well
It were done quickly: if the assassination
Could trammel up the consequence, and catch
With his surcease success; that but this blow
Might be the be-all and the end-all here,
But here, upon this bank and shoal of time,
We'ld jump the life to come."""
```

## escape
* 문자열의 시작과 끝을 알리는 ''는 문자열 중간에 들어가는 경우 에러가 날 수 있음. 
* JAVA 에서와 같이 escape 문을 쓰면됨.(역 슬래시)

```python
my_string = 'It's a lovely day!'
print(my_string)

Output : 
File "main.py", line 1
  my_string = 'It's a lovely day!'
                 ^
SyntaxError : invalid syntax
```

```python
my_string = 'It\'s a lovely day!'

print(my_string)

Output : It's a lovely day!
```

또는 홑따옴표가 들어가는 문자열이 있으면 쌍따옴표로 감싸서 해결할 수 