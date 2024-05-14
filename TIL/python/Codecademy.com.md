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

또는 홑따옴표가 들어가는 문자열이 있으면 쌍따옴표로 감싸서 해결할 수 있음.

```python
my_string = "It's a lovely day!"

print(my_string)
```

자바와 동일하게도 줄바꿈, 탭추가 처럼 \\n \\t 가 있음.

```python
note = "I am on top!\nI am on bottom. \n\tI am indented!"
print(note)

Output : 
I am on top!
I am on bottom.
     I am indented!
```


## 문자열 수정

특별한 연산자가 있음. 예를 들어서 + 는 문자열을 연결하고, * 는 문자열을 곱하는데 사용됨.

```python
string_one = "Hello, "
string_two = "World! "
combo = string_one + string_two

print(combo)
# Output : Hello, World!

new_combo = combo * 2
print(new_combo)
# Output : Hello, World! Hello, World!


if "World" in new_combo"
	print("It's here!")
# Output : It's here!
```

문자열은 아래와 같은걸로도 지정할 수 있음.
* f\\F 플래그
* .format()

**f\\F 플래그**

**.format()**
```python
something = '볼펜'
EA = 2
one_length = 5.343
scale = 'cm'

print('{} {}개의 길이는 {}{} 입니다.'.format(something, EA, one_length*EA, scale))

#실수 포맷팅 소수점 반올림 하기
print('{} {}개의 길이는 {:.2f}{} 입니다.'.format(something, EA, one_length*EA, scale))

출처: [https://firedino.tistory.com/56](https://firedino.tistory.com/56) [F.I.R.E.를 꿈꾸는 공룡 _ FIRE DINO (파공):티스토리]
```