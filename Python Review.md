# Python Review

### 1번

```python
# 시퀀스는 순서를 가지고 있을 뿐, 정렬이 되어있는 것은 아님.
```



### 2번

```python
lunch = ['짜장면', '짬뽕', '탕수육']
lunch[-2][-2]  # 짬
```



### 3번

```python
class Dog:
    num_of_dogs = 0
    def __init__(self):
        Dog.num_of_dogs += 1

dog1 = Dog()
dog2 = Dog()

print(dog2.num_of_dogs)  
# 2 why? 하나의 인스턴스가 생성이 될때마다 class attribute를 1씩 증가시켜라. -> dog1, dog2 생성되었으므로 2
# 인스턴스 어트리뷰트는 클래스 어트리뷰트로 접근 가능 (Dog.num_of_dogs에 접근 가능)
```



### 4번

```python
my_complex = 3 + 4j
my_complex.real  # 3 -> attribute -> my_complex.real() 할 필요 없음
my_complex.imag  # 4j -> print(my_complex.imag) = 4.0(float)이므로 함수로 표현 불가
```



### 5번

```python
def func(c, b, a):
    return a * b + c

print(func(3, 6, 5))  # 33
```





### 6번

```python
print(type({}))  # class dict
```



### 7번

```python
# 함수 작성 시 return 작성을 하지 않으면, 에러가 뜨지는 않음. return 문이 없으면 None을 반환
```



### 8번

```python
# 1을 3개가 든 리스트 만들기  -> numbers = [1, 1, 1]
numbers = [1] * 3

numbers = []
numbers.append(1*3)  # numbers = [3]
```



### 9번

```python
m = 'hello world'
for c in m:
    if c == 'o':
        print(m)
        # 'hello world'
        # 'hello world'
```



### 10번

```python
d1 = {'d': dict()}  # {'d': {}}
d2 = dict(d={})  # {'d': {}}
```



### 11번

```python
a = {'a': 1, 'b': 2}
a.get('a')  # 1
a.get('c')  # None
a.get('c', 'hihi')  # hihi
```



### 12번

```python
def func(c='3', *args):  # c는 값을 받았지만, args에 의해 덮어씌어짐
    a, c, b = args  # args에 '4', '1', '2'가 들어감 -> ('4', '1', '2')
    return a + b + c

print(func('3', '4', '1', '2'))
```



### 13번

```python
name = 'kim'

class Person:
    name = 'lee'

    def greeting(self):
        print(name)  # self.name을 인쇄하는 것이면 lee가 맞음
                     # self가 없음 -> 특정 instance나 class를 볼 수 없음 -> 전역변수에서 찾음(LEGB)

p1 = Person()
p1.name = 'hong'
p1.greeting()  # 위에서 self.name => hong을 출력
```



### 14번

```python
word = 'python'

slicing = word[3:8]

print(slicing)  # hon
```