
## 소수 구하는 방법

```python
# 소수 판별 함수(2이상의 자연수에 대하여)
def is_prime_number(x):
    # 2부터 (x - 1)까지의 모든 수를 확인하며
    for i in range(2, x):
        # x가 해당 수로 나누어떨어진다면
        if x % i == 0:
            return False # 소수가 아님
    return True # 소수임

print(is_prime_number(4)) # 4는 소수가 아님
print(is_prime_number(7)) # 7은 소수임
```

- 모든 약수가 가운데 약수를 기준으로 곱셈 연산에 대해 대칭을 이루는 것을 알 수 있다
- 따라서 우리는 특정한 자연수의 모든 약수를 찾을 때 가운데 약수(제곱근)까지만 확인하면 된다

```python
import math

# 소수 판별 함수
def is_prime_number(x):
    # 2부터 x의 제곱근까지의 모든 수를 확인하며
    for i in range(2, int(math.sqrt(x)) + 1):
        # x가 해당 수로 나누어떨어진다면
        if x % i == 0:
            return False # 소수가 아님
    return True # 소수임

print(is_prime_number(4)) # 4는 소수가 아님
print(is_prime_number(7)) # 7은 소수임
```

## 문제1. 소수찾기

![](https://velog.velcdn.com/images/miracle-21/post/af68fc8b-0f8f-4abd-b6cf-a04a0672cb2c/image.png)

```python
import math

def solution(n):
    result = 0
    for i in range(2,n+1):
        for j in range(2, int(math.sqrt(i))+1):
            if i % j == 0:
                break
        else:
            result += 1
    return result
```

```python
# 다른사람의 풀이
# 에라토스테네스의 체
def solution(n):
    num=set(range(2,n+1))
    for i in range(2,n+1):
        if i in num:
            num-=set(range(2*i,n+1,i)) 
    return len(num)
```

num에 숫자 i가 있으면 본인을 제외한 배수를 제거하면서 소수 판별

## 문제2. 소수 만들기

![](https://velog.velcdn.com/images/miracle-21/post/225ffbc4-19c2-47b7-a411-535a5c1d5664/image.png)

```python
from itertools import combinations
import math

def solution(nums):
    lst = list(map(sum,combinations(nums,3)))
    result = 0
    for i in lst:
        for j in range(2, int(math.sqrt(i))+1):
            if i % j == 0:
                break
        else:
            result += 1
    return result
```

itertools 라이브러리

- 순열(Permutation)
- 조합(Combination)
- 중복 순열

`math.sqrt(i)` 대신 `int(x**0.5)` 으로 대체 가능. 하지만 속도 차이는 얼마 나지 않는다.

---

<이론 출처: [https://freedeveloper.tistory.com/391](https://freedeveloper.tistory.com/391)>