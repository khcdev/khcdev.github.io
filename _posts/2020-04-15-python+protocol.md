---
title:  "python protocol"
search: false
categories: 
  - python
last_modified_at: 2020-02-14T11:00:00+09:00
---


서술 방식
=> 덕 타이핑이 뭔지에 대해 설명하고 예시를 든다 (덕타이핑 예제, 활용용도)
=> 파이썬의 매직매서드를 활용하요 사용자 정의 구문도 리스트처럼 사용할 수 있게 한다.
=> 프렌치덱 예제를 사용 한다.

# Duck Typing

```
Duck Typing - ‘If it walks like a duck and it quacks like a duck, then it must be a duck’
‘오리처럼 걷고, 오리처럼 꽥꽥거리면, 그것은 틀림없이 오리다.’ 
```

``` python
# Duck typing
class Duck:
    def walk_with_2legs(self):
        print('뒤뚱 뒤뚱')

    def quack(self):
        print("꽥꽥")


class MallardDuck:
    def walk_with_2legs(self):
        print('뒤뚱 뒤뚱 뒤뚱')

    def quack(self):
        print("꽥꽥꽥")


class Dog:
    def walk_with_4legs(self):
        pass

    def bark(self):
        print('왈왈')

duck = Duck()
mallard_duck = MallardDuck()
dog = Dog()

duck.quack()
mallard_duck.quack()
duck.walk_with_2legs()
mallard_duck.walk_with_2legs()
dog.quack()


# Result

꽥꽥
꽥꽥꽥
뒤뚱 뒤뚱
뒤뚱 뒤뚱 뒤뚱
Traceback (most recent call last):
  File "...", line 36, in <module>
    dog.quack()
AttributeError: 'Dog' object has no attribute 'quack'

```

* 파이썬, 루비같은 동적언어의 특징으로 본질적으로 다른클래스라도 객체의 적합성은 객체의 실제 유형이 아니라 특정 메소드와 속성의 존재에 의해 결정됨
* 속성과 메소드 존재에 의해 객체의 적합성이 결정된다.


# Python magic method 활용 하여 시퀀스 사용자 정의 시퀀스 생성해보기

## Maginc Method


# python 내장 시퀀스

## Sequence?
* 데이터를 순서대로 하나씩 나열하여 나타낸 데이터 구조
* 특정 위치(~번째)의 데이터를 가리킬 수 있다.

**데이터 참조에 따른 분류**
* 컨테이너 시퀀스

    `list, tuple collections.deque` 등
* 균일 시퀀스

    `str, bytes, bytearray, memoryview` 등


**가변성에 따른 분류**
* 가변 시퀀스

    `list, bytearray, array.array, collections.deque, memoryview`


* 불변 시퀀스

    `tuple, str, bytes`


