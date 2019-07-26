# Python 

### 1. 변수 x와 y 바꾸기

```python
x, y = 1, 2
x, y = y, x
```



### 2. float 부동소수점 사용

```python
# floating point rounding error
# print(type(a)), print(type(b)) 하면 a, b 모두 float이다. 이때, 컴퓨터는 표현 과정에서 부동소수점을 사용하기때문에 항상 같은 값으로 일치되지 않는다.
a = 0.1 * 3
b = 0.3
# 1번( Good )
import math
math.isclose(a, b)
# 2번 (기본)
abs(a - b) <= 1e-10  #0.00000001정도만 차이난다면 a와 b는 같다고 해라
```



### 3. bool

```python
# False
bool(0), bool(None), bool([]), bool('')
# True
bool(1), bool([1, 2, 3]), bool(['hi']), bool('hi')
```



### 4. str(문자열)

```python
# 문자열 작성시 가장 많이 사용
f'Hello {name}'
```

```python
# 가로 n, 세로 m 인 직사각형 만들기
n = 5
m = 9
print(('*' * n + '\n') * m)
# print(('*' * n \n) * m)은 오류가 난다. 
	#why? 1. '*'은 str이다. \n도 str처리를 해야함
	#     2. '*'뒤에 \n이 붙어있어야 하나가 되고 그것이 9번 곱해짐
```



### 5.  산술 연산자

```python
# divmod는 나눗셈과 관련된 함수
print(divmod(5, 2)) # 몫, 나머지
```



### 6. 논리 연산자

```python
# 파이썬에서 and는 a가 거짓이면 a를 리턴
print(3 and 5) # 3이 참이므로 5가 나옴 -> True
print(3 and 0) # 3이 참이므로 0이 나옴 -> False
print(0 and 3) # 0이 거짓이므로 0이 나옴 -> False
print(0 and 0) # 0이 거짓이므로 0(앞) 나옴 -> False

# 파이썬에서 or은 a가 참이면 a를 리턴
print(3 or 5) # 3이 참이므로 3가 나옴 -> True
print(3 or 0) # 3이 참이므로 3이 나옴 -> True
print(0 or 3) # 0이 거짓이므로 3이 나옴 -> True
print(0 or 0) # 0이 거짓이므로 0(뒤) 나옴 -> False
```



### 7. 변환

```python
# int() : string(정수인 경우), float를 int로 변환
# float() : string, int를 float로 변환
# str() : int, float, list, tuple, dictionary를 문자열로 변환 ex. int('3.5') 불가
```



### 8. 튜플

```python
x, y = 1, 2  #튜플 처리
```



### 9. 시퀀스에서 활용할 수 있는 연산자/함수

```python
# 1. s1 + s2 하려면 type이 같아야한다!
str() + str()
# 2. 숫자 0이 6개 있는 list
[0] * 6   # [0, 0, 0, 0, 0, 0]
# 3. 두번째, 세번째 값만 가지고 오기
locations[1:3]
# 4. 0부터 30까지의 숫자를 3씩 증가시킨 상태
r = list(range(30)) #1부터 숫자를 세면 30 포함, 0부터 숫자를 세면 30 미포함
result = r[0:len(r):3]
print(result)
```



### 10. 딕셔너리

```python
# dictionary는 중복된 key는 존재할 수가 없다.
a = {
    1: 1,
    2: 2,
    3: 3,
    1: 4,
}
print(a)  # 더 밑에 나와있는 값으로 덮어버림 {1: 4, 2: 2, 3: 3}
```



### 11. Sum 함수

```markdown
a = [], {}, () 다 사용 가능!
```

