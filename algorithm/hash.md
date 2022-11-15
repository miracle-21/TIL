- [사전 자료형](#사전-자료형)
- [문제1: 완주하지 못한 선수](#문제1-완주하지-못한-선수)
- [문제2. 폰켓몬](#문제2-폰켓몬)
- [문제3. 전화번호 목록](#문제3-전화번호-목록)
- [문제4. 위장](#문제4-위장)


#

**⭐⭐⭐⭐ dict**</br>
**⭐⭐⭐ set**</br>
**⭐ slice**</br>
**⭐ enumerate()**

#

# 사전 자료형

- **키(Key)와 값(Value)의 쌍을 데이터로 가지는 자료형이다.**
- **변경 불가능한(Immutable) 자료형을 키로 사용한다.**
- 파이썬의 사전 자료형은 해시 테이블(Hash Table)을 이용한다.
- 므로 데이터의 조회 및 수정에 있어서 O(*1*)의 시간에 처리 할 수 있다.

```python
data = dict()
data['사과'] = 'Apple'
data['바나나'] = 'Banana'
data['코코넛'] = 'Coconut'

# 키 데이터만 담은 리스트
key_list = data.keys()
print(key_list)
>>> dict_keys(['사과', '바나나', '코코넛'])

# 값 데이터만 담은 리스트
value_list = data.values()
print(value_list)
>>> dict_values(['Apple', 'Banana', 'Coconut'])

# 각 키에 따른 값을 하나씩 출력
for key in key_list:
    print(data[key])
>>> Apple
		Banana
		Coconut
```

# 문제1: 완주하지 못한 선수
![](https://velog.velcdn.com/images/miracle-21/post/cd2b1621-6298-4b3b-b46c-a9034bf4b368/image.png)

```python
def solution(participant, completion):
    dict = {}
    for i in participant:
        try:
            dict[i] += 1
        except:
            dict[i] = 1
    for i in completion:
        dict[i] -= 1
    for key, value in dict.items():
        if value != 0:
            return key
```

dictionary에 선수를 하나씩 넣고 완주한 선수를 빼고 남은 값 return.

```python
#효율성테스트 실패
def solution(participant, completion):
    if len(participant) == len(set(participant)):
        return (list(set(participant) - set(completion)))[0]
    else:
        dict = {}
        for i in participant:
            try:
                dict[i] += 1
            except:
                dict[i] = 1
        for key, value in dict.items():
            if completion.count(key) != value:
                return key
```

if문으로 쓴 코드는 안쓰는게 더 빠르다.

그리고 count 함수로 개수를 비교하는 것보다 for문 돌려서 value 값을 빼는게 더 빠르다.

**dictionary 자료형을 사용한 문제.**

# 문제2. 폰켓몬
![](https://velog.velcdn.com/images/miracle-21/post/c73fa74c-752c-4aef-a7b1-785467d8070c/image.png)

```python
def solution(nums):
    if len(set(nums)) >= len(nums)/2:
        return len(nums)/2
    else:
        return len(set(nums))
```

**set 자료형을 이용한 문제.**

# 문제3. 전화번호 목록
![](https://velog.velcdn.com/images/miracle-21/post/50c1b543-b5dd-4098-a593-50afae7c74b9/image.png)

```python
def solution(phone_book):
    phone_book.sort()
    for i in range(1, len(phone_book)):
        if phone_book[i-1] != phone_book[i][0:len(phone_book[i-1])]:
            continue
        elif phone_book[i-1] in phone_book[i]:
            return False
    return True
```

전화번호 전체가 다른 전화번호의 접두어가 되어야 한다.

앞의 전화번호가 뒤의 전화번호 맨 앞에 온전히 포함되어야 한다.

**slice를 이용한 문제.**

```python
# deque 사용. 느리다.
from collections import deque

def solution(phone_book):
    phone_book.sort()
    q = deque(phone_book)
    while len(q) > 1:
        num = q.popleft()
        if num == q[0][:len(num)]:
            return False
    return True
```

# 문제4. 위장
![](https://velog.velcdn.com/images/miracle-21/post/315e01de-5530-470c-90ac-0ccc5e600df5/image.png)

```python
def solution(clothes):
    dict = {}
    for i in clothes:
        try:
            dict[i[1]] += 1
        except:
            dict[i[1]] = 1
    num = 1
    lst= []
    for key, value in dict.items():
        num *= (value+1)
    return num-1
```

**(의상종류+1)을 모두 곱한 후 -1**

의상종류가 3개면 각각의 부위에서 안입는것,첫번째,두번째,세번째 총 4개의 선택이 가능하다.

부위별로 가능한 선택 수를 곱하면 모든 조합이 나오는데, 하나도 안 입는 경우 1은 뺀다.

**dictionary 자료형 사용. 조합(combination) 문제라고 한다.**

---

<이론 출처>

[https://freedeveloper.tistory.com/360](https://freedeveloper.tistory.com/360)