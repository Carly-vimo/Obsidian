
### 함수 (Function)
- 함수를 정의할 때 **def** 사용
- 함수는 왜 사용할까 ? : **코드의 재사용을 위해** 

[함수의 두 가지 작업]
1. 정의하기 : 0 또는 1개 이상의 매개 변수를 갖는다. 
2. 호출하기 : 0 또는 1개 이상의 결과를 얻는다. 
	함수를 호출할 때는 **()** 를 사용한다. 

[참고]

IF 조건문에서 함수를 호출하여 반환되는 값으로 조건 테스트가 가능 
``` python
if agree() : 
	print("Splendid!")
else: 
	print("unexpected")
```



### 인수와 매개변수 
- 함수 밖에서는 '인수'라고 하지만 함수 내부에서는 '매개변수' 라고 함 

[아무것도 없다는 의미의 None]
None : 아무것도 없다는 의미의 파이썬의 특별한 값 
- **불리언의 False와 다른 값을 의미** 
- 아무 것도 없는 빠진 빈 값을 구분하기 위해서 None을 사용 
- 정수 0, 부동소수점 0.0, 빈 문자열, 빈 리스트, 빈 튜플, 빈 딕셔너리, 빈 셋 : **모두 False지만 None은 아님.** 


#### 위치 인수
- 인수의 가장 익숙한 유형 > 값을 순서대로 상응하는 매개변수에 복사하는 위치 인수 
- 가장 일반적이지만 인수의 각 위치와 의미를 알아야한다는 단점

#### 키워드 인수 
- 위치 인수의 혼란을 피하기 위해 매개변수에 상응하는 이름을 인수에 지정할 수 있음. 
- 인수를 함수의 정의와 다른 순서로도 지정이 가능하다.

* 만약 위치 인수와 키워드 인수 모두 이용해 함수를 호출한다면, **위치 인수가 먼저 와야함** 

#### 기본 매개 변수 지정하기
- 매개 변수에 기본 값을 지정할 수 있음. 
- 함수를 호출할 때 대응하는 인수를 제공하지 않으면 기본값을 사용한다. 
- 만약 기본값 대신 대응하는 인수가 존재한다면, 그 인수가 사용됨. 

> [!NOTE]
> 기본 인수는 함수가 실행될 때 계산되지 않고, 함수를 정의할 때 계산된다.
> 리스트 혹은 딕셔너리와 같은 가변 데이터 타입을 기본 인수로 사용할 때 실수하게 됨 

원하는 내용 : 함수를 호출할 때마다 하나의 값이 들어있는 리스트를 리턴 받고 싶음
``` python 
def buggy(arg, result = []):
	result.append(arg)
	print(result)

```
함수를 정의할 때, 즉 한 줄 씩 불러올 때 이미 빈 리스트가 정의되어버림. 
호출할 때마다 리스트가 새로 갱신되는 것이 아닌 이미 정의된 빈 리스트에 계속 값을 넣는 형태가 되어버림

그렇다면, 원하는 내용대로 값을 리턴 받으려면 어떻게 해야할까? 
``` python
def buggy(arg):
	result = [] 
	result.append(arg)
	print(result)


```

#### \*args
> 위치 인수 분해하기 / 모으기 
- 함수의 매개변수에 애스터리스크를 사용할 때, 애스터리스크는 매개변수에서 위치 인수 변수를 튜플로 묶는다.
``` python 
def print_args(*args):
	print("positional tuple :" ,args)

print_args(1,2,3,4,5,6)
#positional tuple :(1,2,3,4,5,6)
# 값을 각각 부여했지만 하나의 튜플로 모아서 반환해줌 
```
- 가변 인수를 사용하는 print 함수같은 경우 매우 유용함 
```python

def print_more(one, two, *args):
	print("one is " , one)
	print("two is " , two)
	print("all rest is " , args)

```
- 즉 정리해보면, \*args는 함수 외부에서 분해된 값을 함수 내부에서 튜플로 모아주는 역할임. 


#### \*\*kwargs
> 키워드 인수 분해하기 / 모으기 
- 키워드 인수를 묶기 위해 두 개의 애스터리스크를 사용할 수 있다. 
- 두 개의 애스터리스크를 사용할 때는 키워드 인수를 딕셔너리로 묶는 역할을 한다
``` python
def print_kwargs(**kwargs):
	print("keyword arguments :" , kwargs)

```
```python
print_kwargs(wine= "merlot", entree = "mutton", dessert = "macaroon" )
# keyword arguments : {'wine': 'merlot', 'entree': 'mutton', 'dessert': 'macaroon'} 
# 각각의 값을 이름 = 값의 형태로 분해해서 넣었지만 하나의 딕셔너리로 묶어서 반환해줌 

```
- 키워드 인수를 함수에 전달하면, 함수 내 키워드 매개변수와 일치함 -> 그에 맞는 값으로 지정되어 출력
- 딕셔너리 인수를 함수에 전달하면 함수 내 딕셔너리 매개변수가 있다 -> \*\*kwargs
- 하나 이상의 키워드 인수 (이름 = 값)를 함수에 전달하고 이를 \*\*kwargs가 수집 -> 딕셔너리로 반환 
- 함수 외부에서 \*\*kwargs 는 딕셔너리 kwargs를 **이름= 값**의 형태로 분해함.
- 함수 내부에서 단일 딕셔너리 매개변수 kwargs로 모은다. 


#### DocString
- 함수 바디 시작 부분에 문자열을 포함시켜 함수 정의에 대한 문서를 붙일 수 있음. 
- docstring을 길게 작성할 수도 있고, 포매팅을 추가할 수도 있음. 
```python 
def print_if_true(thing, check):
	'''
	prints the first argument if a second argument is true 
	The operation is : 
		1. Check whether the *second* argument is true. 
		2. If it is, print the *first* argument. 
		이 부분에서 포매팅이 되는 것 같은데 현재 3.9.6에서는 적용이 안됨 
	'''
	if check : 
		print(thing)

```
- 서식 없는 독스트링 그대로 보고 싶으면 \_\_doc\_\_ 를 사용하면 된다.
```python
print(print_if_ture.__doc__)
```
- 더블 언더바는 파이썬에서 **내부 사용 목적으로 만들어진 변수**임. 


#### 파이썬에서 함수의 다양한 기능 
> **파이썬에서 모든 것은 객체다**
> 파이썬에서 사용되는 숫자, 문자열, 튜플, 리스트, 딕셔너리, 함수 모두 객체라는 의미다. 

함수 안에 매개변수로 (함수, 변수)의 조합으로 넣을 수도 있음. 

```python 
def add (arg1 , arg2):
	print(arg1 + arg2)

def sum(*args):
	return sum(args)

def run_something(func, arg1, arg2):
	func(arg1 , arg2)

def run_args(func, *args):
	return func(*args)

run_something(add, 1, 2)
# 3 

run_args(sum , 1,2,3,4,5)
# 15 

```

### 내부 함수 
- 함수 안에 또 다른 함수를 정의할 수 있음.
- 내부 함수는 반복문이나 코드 중복을 피하고자 또 다른 함수 내에 어떤 복잡한 작업을 한 번 이상 수행할 때 유용하게 사용됨. 
```python 

def knights(saying):
	def inner(quote):
		return "We are the knights who says : '%s'" %quote
	return inner(saying)

```
> 위 함수의 동작 과정
> 1. knights() 함수가 inner(saying) 함수 리턴 
> 2. inner() 함수가 knights의 매개변수를 받아 값을 리턴 


#### 클로저 (Closure)

- 내부 함수는 클로저처럼 동작할 수 있다.  -> 클로저는 다른 함수에 의해 동적으로 생성된다. 
- 그리고 외부 함수로부터 생성된 변수값을 변경하고 저장할 수 있는 함수다.

``` python
def knights2(saying):
	def inner2():
		return "Wer are the knights who say : '%s'" %saying
	return inner2 

```
- 위 예제를 보면 내부에 있는 inner2 함수는 knights2 함수의 인수를 알고서 return 해준다.
- 이것이 외부 함수에 의해 동적으로 생성되고 그 함수의 변수값을 알고 있는 함수가 **클로저**임. 


### Lambda
- 람다 함수는 **단일 문장으로 표현되는 익명의 함수**다. 
- 람다는 인수를 취하지 않거나 콤마로 구분된 인수를 취하고 콜론 (:) 이후에 함수를 정의한다.
``` python 
stairs = ["thud", "meow", "thud", "meow"]
edit_story(stairs , lambda word : word.caplitalize() + "!" ) 
```
- 함수를 굳이 하나 더 정의하지 않고도 lambda 한 줄로 간략하게 표현이 가능하다.
- 위 예제에서는 word라는 하나의 인수만 받았는데 여러 개 인수도 받기 가능하다
- lambda 를 사용할 때는 ()를 적지 않는다. 
- 람다는 **많은 작은 함수를 정의하고 이들을 호출해서 얻은 모든 결과값을 저장해야하는 경우 유용**하다. 


### 제너레이터
- 제너레이터는 시퀀스를 생성하는 객체
- 제너레이터로 전체 시퀀스를 한 번에 메모리에 생성하고 정렬할 필요 없이 잠재적으로 아주 큰 시퀀스를 순회할 수 있다. 
- 제너레이터는 이터레이터에 대한 데이터의 소스로 자주 사용됨 
- 제너레이터 중 대표적인 예 ex) range
- 제너레이터는 순회할 때마다 마지막 호출된 항목을 기억하고 다음 값을 반환
	- how? return 키워드 대신 **yield** 라는 키워드를 사용하는 함수
	- 일반 함수의 경우 이전 호출에 대한 메모리가 없고 항상 똑같은 상태로 첫번째 줄부터 실행
	- yield를 사용하게 되면 결과값을 돌려주지만 실행한 상태를 그대로 저장한 후 잠깐 멈추기 가능
	- 나중에 멈춘 상태에서부터 이어서 코드를 실행할 수 있음
``` python
def my_range(first = 0 , last = 10 , step = 1):
	number = first
	while number < last: 
		yield number 
		number += step

# 제너레이터 객체 생성
ranger = my_range()

num1 = next(ranger)
num2 = next(ranger)

print(num1, num2)

```
- yield가 사용된 함수는 () 를 붙여도 바로 실행되지 않음 -> 따라서 generator 객체만 찍혀서 나옴
	- 대신 제너레이터가 실행될 준비를 하게 됨
- 제너레이터 객체를 생성했다면 next 함수 호출을 통해서 제너레이터 객체 내의 코드를 실행할 수 있음. 
	- 이 때 yield 구문을 만나면 yield 키워드에 있는 값을 호출부로 리턴해주고 실행의 흐름도 호출부로 이동하게 된다. (+ 파이썬의 일반 함수와는 다르게 현재 상태를 그대로 유지가 가능함)
	- 코드가 중지된 시점을 유지하고 있기 때문에 해당 상태로부터 다시 코드를 이어서 실행이 가능함. 

- next()를 사용하지 않고 제너레이터로부터 값을 가져오는 쉬운 방법은 for문을 사용하는 방법
	- for문을 사용하면 반복할 때마다 내부적으로 next()를 호출하는데 값이 끝날 때까지 가져오게 됨
	- 제너레이터 객체로부터 순차적으로 값을 가져오게 되는 것 
```python 
def num_gen():
	for i in range(6):
		yield i 

gen = num_gen()

for i in gen:
	print(i)

```
#### 제너레이터 대체 왜 사용하는걸까?
- 제너레이터를 사용하게 되면 한 번에 데이터를 모아서 처리하지 않기 때문에 큰 메모리를 사용하지 않아도 되는데 이는 규모가 있는 프로그램을 개발할 때 중요한 요소임. 
- 큰 규모의 확장성이 있는 프로그램을 개발하기 위해서 사용한다 
- 빵 100개 굽고 포장하는 상황이라고 가정했을 때 
	- 일반 함수의 경우
		- 빵 100개 굽는 동안 포장 직원은 멍때리기 
		- 빵 100개 굽기 완료! 포장 직원 1개씩 일하기 
	- 제너레이터의 경우
		- 빵 1개 굽고 포장 직원 포장하기 
		- 빵 1개 굽고 포장 직원 포장하기 

- 빵 굽고 포장하는 경우로 가정했을 때 한 번에 데이터를 모아서 처리하지 않고 그 때 그 때 처리하므로 많은 메모리를 먹지 않음

#### 제너레이터 컴프리헨션
- 제너레이터 컴프리헨션은 제너레이터 함수의 축약 버전
- 안보이게 yield 문을 실행하고 제너레이터 객체를 반환한다.
```python
genobj = (pair for pair in zip(['a','b'] , [1, 2]))
print(genobj)
```


### 데코레이터 
- 
