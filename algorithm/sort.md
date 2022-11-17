- [정렬 알고리즘](#정렬-알고리즘)
  * [1. 선택 정렬: ***O(N²)***](#1-선택-정렬-on²)
  * [2. 삽입 정렬: ***O(N²), O(N)(최선)***](#2-삽입-정렬-on²-on최선)
  * [3. 퀵 정렬: ***O(NlogN), O(N²)(최악)***](#3-퀵-정렬-onlogn-on²최악)
  * [4. 계수 정렬: *O(N + K)*](#4-계수-정렬-on--k)
- [문제1: K번째수](#문제1-k번째수)
- [문제2. 가장 큰 수](#문제2-가장-큰-수)
- [문제3: H-Index](#문제3-h-index)


# 정렬 알고리즘

- 데이터를 특정한 기준에 따라 순서대로 나열하는 것.

## 1. 선택 정렬: ***O(N²)***

- 가장 작은 데이터를 선택해 맨 앞에 있는 데이터와 바꾸는 것을 반복한다.

```python
array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

for i in range(len(array)):
    min_index = i # 가장 작은 원소의 인덱스
    for j in range(i + 1, len(array)):
        if array[min_index] > array[j]:
            min_index = j
    array[i], array[min_index] = array[min_index], array[i] # 스와프

print(array)
>>> [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## 2. 삽입 정렬: ***O(N²), O(N)(최선)***

- 처리되지 않은 데이터를 하나씩 골라 적절한 위치에 삽입한다.
- 데이터를 한 칸씩 왼쪽으로 이동하여 자기보다 작은 데이터를 만나면 멈춘다.

```python
array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

for i in range(1, len(array)):
    for j in range(i, 0, -1): # 인덱스 i부터 1까지 1씩 감소하며 반복하는 문법
        if array[j] < array[j - 1]: # 한 칸씩 왼쪽으로 이동
            array[j], array[j - 1] = array[j - 1], array[j]
        else: # 자기보다 작은 데이터를 만나면 그 위치에서 멈춤
            break

print(array)
>>> [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## 3. 퀵 정렬: ***O(NlogN), O(N²)(최악)***

- 기준 데이터를 설정하고 그 **기준보다 큰 데이터와 작은 데이터의 위치를 바꾸는 방법**이다.
- 일반적인 상황에서 가장 많이 사용되는 정렬 알고리즘 중 하나이다.
- 병합 정렬과 더불어 대부분의 프로그래밍 언어의 정렬 라이브러리의 근간이 되는 알고리즘이다.
- 가장 기본적인 퀵 정렬은 **첫 번째 데이터를 기준 데이터(Pivot)로 설정**한다.

```python
array = [5, 7, 9, 0, 3, 1, 6, 2, 4, 8]

def quick_sort(array, start, end):
    if start >= end: # 원소가 1개인 경우 종료
        return
    pivot = start # 피벗은 첫 번째 원소
    left = start + 1
    right = end
    while(left <= right):
        # 피벗보다 큰 데이터를 찾을 때까지 반복 
        while(left <= end and array[left] <= array[pivot]):
            left += 1
        # 피벗보다 작은 데이터를 찾을 때까지 반복
        while(right > start and array[right] >= array[pivot]):
            right -= 1
        if(left > right): # 엇갈렸다면 작은 데이터와 피벗을 교체
            array[right], array[pivot] = array[pivot], array[right]
        else: # 엇갈리지 않았다면 작은 데이터와 큰 데이터를 교체
            array[left], array[right] = array[right], array[left]
    # 분할 이후 왼쪽 부분과 오른쪽 부분에서 각각 정렬 수행
    quick_sort(array, start, right - 1)
    quick_sort(array, right + 1, end)

quick_sort(array, 0, len(array) - 1)
print(array)
>>> [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## 4. 계수 정렬: *O(N + K)*

- 특정한 조건이 부합할 때만 사용할 수 있지만 **매우 빠르게 동작하는** 정렬 알고리즘이다.
- 계수 정렬은 데이터의 크기 범위가 제한되어 정수 형태로 표현할 수 있을 때 사용 가능하다.
- 데이터의 개수가 𝑁, 데이터(양수) 중 최댓값이 𝐾일 때 최악의 경우에도 수행 시간 ***O(N + K)*** 를 보장한다.

```python
# 모든 원소의 값이 0보다 크거나 같다고 가정
array = [7, 5, 9, 0, 3, 1, 6, 2, 9, 1, 4, 8, 0, 5, 2]
# 모든 범위를 포함하는 리스트 선언 (모든 값은 0으로 초기화)
count = [0] * (max(array) + 1)

for i in range(len(array)):
    count[array[i]] += 1 # 각 데이터에 해당하는 인덱스의 값 증가

for i in range(len(count)): # 리스트에 기록된 정렬 정보 확인
    for j in range(count[i]):
        print(i, end=' ') # 띄어쓰기를 구분으로 등장한 횟수만큼 인덱스 출력
>>> 0 0 1 1 2 2 3 4 5 5 6 7 8 9 9
```

# 문제1: K번째수
![](https://velog.velcdn.com/images/miracle-21/post/7b30c2a2-1b7c-4b92-a517-b2912f68678f/image.png)

```python
def solution(array, commands):
    answer = []
    for i in commands:
        answer.append(sorted(array[i[0]-1:i[1]])[i[2]-1])
    return answer
```

**slice, sort 사용.**

# 문제2. 가장 큰 수
![](https://velog.velcdn.com/images/miracle-21/post/f60cc3de-a3ec-4b68-b2d6-769b18e64847/image.png)

```python
def solution(numbers):
    lst = []
    answer = ''
    for i in numbers:
        lst.append(str(i))
    lst.sort(key = lambda x : x*3, reverse=True)
    for i in lst:
        answer += i
    return str(int(answer))
```

key 인자에 함수를 넘겨주면 우선순위가 정해진다.

numbers의 자릿수는 최대 3자리니까 3을 곱했다.

**lambda, key sort 사용. 센스가 중요한 문제.**

# 문제3: H-Index
![](https://velog.velcdn.com/images/miracle-21/post/8460c591-a8a9-4f38-9aa2-81e52585c09f/image.png)

```python
# 나의풀이
def solution(citations):
    citations.sort()
    for i in citations:
        if i >= len(citations[citations.index(i):]):
            return len(citations[citations.index(i):])
    return 0
```

오름차순 정렬 후, 논문 i의 인용 횟수가 i 이후의 논문 개수보다 크면 i 이후의 논문 개수가 최댓값이 된다. 다른 사람의 풀이에서 힌트를 얻었다.

```python
# 다른 사람의 풀이
def solution(citations):
    citations.sort(reverse=True)
    for i in range(len(citations)):
        if citations[i] < i+1:
            return i
    return len(citations)
```

**sort 사용.**

---

<이론 출처>

[https://freedeveloper.tistory.com/274](https://freedeveloper.tistory.com/274)