---
layout: post
title:  "Python module: Collections"
date:   2019-11-07
excerpt: "파이썬 콜렉션 모듈 써보기"
tag:
- python
- module
- collections
comments: false
---

평소처럼 문제를 풀다가 파이썬 collections 모듈에 있는 Counter의 신박한 기능을 발견했다.

먼저 Counter란 리스트에 대해서 각 요소가 몇 개씩 있는지 셀 때 쓰는 클래스이다.

예를 들면
```python
from collections import Counter
a = 'aaabbbbbccccccccc'
b = 'aabbbbbcccc'

a_count = Counter(a)
b_count = Counter(b)
print(a_count)
#Counter({'c': 9, 'b': 5, 'a': 3})
print(b_count)
#Counter({'b': 5, 'c': 4, 'a': 2})
```
이런 식으로 각 요소의 개수를 표현해준다.


생김새도 그렇고 딕셔너리랑 비슷하게 바꿔주는 클래스인줄 알았는데 조금 다른 **카운터 객체** 로 생성하고 이 객체만의 특성이 있다는 것을 알았다.
```python
c = {'a': 1, 'b':2}
d = {'a': 1, 'b':1}
print(a_count-b_count)
#Counter({'c': 5, 'a': 1})
print(c-d)
#TypeError: unsupported operand type(s) for -: 'dict' and 'dict'
```
Counter 객체의 경우요소의 개수이므로 value 값으로 0을 가질 수가 없는 것을 알 수 있고 value에 대해서 사칙연산이 가능하다. 반면에 딕셔너리는 사칙연산이 안되는것을 볼 수 있다.


[관련문제](https://programmers.co.kr/learn/courses/30/lessons/42576)

이걸 풀때 단순히 2개의 리스트를 정렬해서 겹치지 않은게 나오면 바로 리턴해주는 방식으로 풀었는데, 카운터를 쓰면 훨씬 더 짧아지고 시간도 빨라진다.


```python
def solution(participant, completion):
    p = sorted(participant)
    c = sorted(completion)
    for i in range(len(p)-1):
        if p[i] != c[i]:
            return p[i]
    return p[-1]
```
이렇게 풀어도 통과하긴 하지만
```python
import collections

def solution(participant, completion):
    answer = collections.Counter(participant) - collections.Counter(completion)
    return list(answer.keys())[0]
```
훨씬 간결하고 pythonic 하다..!
