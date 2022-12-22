- [스택 : 선입후출](#스택--선입후출)
- [큐 : 선입선출](#큐--선입선출)
- [문제1: 올바른 괄호](#문제1-올바른-괄호)
- [문제2: 같은 숫자는 싫어](#문제2-같은-숫자는-싫어)
- [문제3: 기능개발](#문제3-기능개발)
- [문제4: 프린터](#문제4-프린터)
- [문제5: 다리를 지나는 트럭](#문제5-다리를-지나는-트럭)
- [문제6. 주식가격](#문제6-주식가격)

#
 
**⭐⭐⭐ .append()** </br>
**⭐⭐⭐ .pop() ⇒ pop(0) == deque.popleft()** </br>
**⭐⭐ deque** </br>
**⭐ 빈 배열을 슬라이싱 할 때는 [-1:]** 

#

# 스택 : 선입후출

```python
stack = []

stack.append(5) #5
stack.append(2) #5-2
stack.append(3) #5-2-3
stack.append(7) #5-2-3-7
stack.pop()     #5-2-3
stack.append(1) #5-2-3-1
stack.append(4) #5-2-3-1-4
stack.pop()     #5-2-3-1

print(stack) # 최하단 원소부터 출력
>>> [5, 2, 3, 1]
print(stack[::-1]) # 최상단 원소부터 출력
>>> [1, 3, 2, 5]
```

# 큐 : 선입선출

```python
from collections import deque 

# 큐(Queue) 구현을 위해 deque 라이브러리 사용
queue = deque()

queue.append(5) #5
queue.append(2) #5-2
queue.append(3) #5-2-3
queue.append(7) #5-2-3-7
queue.popleft() #2-3-7
queue.append(1) #2-3-7-1
queue.append(4) #2-3-7-1-4
queue.popleft() #3-7-1-4

print(queue) # 먼저 들어온 순서대로 출력
>>> deque([3, 7, 1, 4])
queue.reverse() # 다음 출력을 위해 역순으로 바꾸기
print(queue) # 나중에 들어온 원소부터 출력
>>> deque([4, 1, 7, 3])
```

# 문제1: 올바른 괄호
![](https://velog.velcdn.com/images/miracle-21/post/7274c304-f831-4411-ac11-19743adf9997/image.png)
```python
def solution(s):
    x = 0
    for i in s:
        if x < 0:
            break
        if i =="(":
            x += 1
        elif i ==")":
            x -= 1
    return x == 0
```

`)`가 `(`보다 앞에 있으면 어차피 `false`기 때문에 `if x<0: break` 조건이 먼저 붙는다.

어찌보면 **append(+)와 pop(-)을 번갈아가며 쓰는 문제.**

# 문제2: 같은 숫자는 싫어
![](https://velog.velcdn.com/images/miracle-21/post/1b39053d-5d4e-484c-b678-a6b8d66a50a0/image.png)

```python
def solution(arr):
    answer = []
    for i in arr:
        if answer[-1:] != [i]:
            answer.append(i)
    return answer
```

처음에는 `try~except`문을 써서 빈 배열을 슬라이싱 했을때 에러가 나타나는 문제를 해결했는데 `[-1:]`로 슬라이싱하면 해결된다는걸 알게됐다.

**append를 사용한 문제.**

# 문제3: 기능개발
![](https://velog.velcdn.com/images/miracle-21/post/c4fa7377-a482-4b49-ac44-0a92ac777736/image.png)

```python
#나의 풀이. 속도가 느리다.
def solution(progresses, speeds):
    num = 0
    time = 0
    answer = []
    while progresses:
        while progresses[0] < 100:
            progresses[0] += speeds[0]
            num += 1
        progresses.pop(0)
        speeds.pop(0)
        if time >= num:
            answer[-1] += 1
        else:
            time = num
            answer.append(1)
        num = 0
    return answer
```

```python
#다른 사람의 풀이
def solution(progresses, speeds):
    answer = []
    time = 0
    count = 0
    
    while len(progresses)> 0:
        if (progresses[0] + time*speeds[0]) >= 100: 
            progresses.pop(0)
            speeds.pop(0)
            count += 1
            
        else:
            if count > 0:
                answer.append(count)
                count = 0
            time += 1
    answer.append(count)
    return answer
```

나의 풀이는 `while`문이 2개나 있어서 실행 속도가 느리다.

`progresses[0]`이 100 이상이 되는 날을 구하고, 앞의 작업보다 빨리 끝나면 `answer += 1`, 늦게 끝나면 다른 날에 배포가 되니 `answer.append(count)`를 했다.

다른사람의 풀이는 앞의 작업과의 속도를 비교하기 위해 time 변수를 사용했다. 앞의 작업이 끝난 날에 100 이상이 되면 바로 `count += 1`을 한다. 아닌 작업은 앞의 작업보다 늦게 끝나고, 다른 날에 배포가 되니 `count = 0` 으로 초기화한다.

**append와 pop을 쓰는 문제.** 센스가 중요한 문제같다.

# 문제4: 프린터
![](https://velog.velcdn.com/images/miracle-21/post/3767438e-5e2a-4d27-bf3b-4d9514284105/image.png)
```python
#deque 모듈 사용
from collections import deque

def solution(priorities, location):
    dq = deque([(i,l) for l, i in enumerate(priorities)])
		# dq = deque([(priorities[0],0), (priorities[1],1), ...])
    answer = 0

    while dq:
        item = dq.popleft()
        if dq and max(dq)[0] > item[0]:
            dq.append(item)
        else:
            answer += 1
            if item[1] == location:
                break
    return answer
```

`enumerate()` 함수는 인덱스와 원소로 이루어진 tuple을 만들어준다.

deque의 첫 번째 값을 빼낸 후(`pop`),  deque의 최댓값보다 작으면 deque에 다시 넣는다(`append`).

deque의 최댓값보다 크면 문서를 출력하고(`answer += 1`) 요청한 문서번호(location)와 일치하면 return 한다. `answer`의 값을 통해 요청한 문서의 출력 순서를 알 수 있다.

```python
#deque 모듈을 사용하지 않는 경우
def solution(priorities, location):
    lst = [(i,l) for l, i in enumerate(priorities)]
    answer = 0

    while lst:
        item = lst.pop(0)
        if lst and max(lst)[0] > item[0]:
            lst.append(item)
        else:
            answer += 1
            if item[1] == location:
                break
    return answer
```

위 코드는 deque를 굳이 사용하지 않아도 풀 수 있다. 평균적으로 이 코드가 더 빠르다.

**append, pop, 또는 deque를 쓰는 문제.**

# 문제5: 다리를 지나는 트럭
![](https://velog.velcdn.com/images/miracle-21/post/5d1be811-2619-4fe1-84a6-efc90ab989da/image.png)
```python
def solution(bridge_length, weight, truck_weights):
    time = 0
    q = [0] * bridge_length
    while q:
        q.pop(0)
        time += 1
        if truck_weights:
            if sum(q) + truck_weights[0] <= weight:
                q.append(truck_weights.pop(0))
            else:
                q.append(0)
    return time
```

다리 위의 무게가 최대 무게보다 가벼워지는 순간 다시 트럭이 지나갈 수 있으니 1초씩 계산해야 한다.

```python
q = [0] * bridge_length
```

다리 길이 만큼의 0을 가진 리스트를 만든다. 리스트의 0의 개수는 다리의 길이다.

```python
while q:
    q.pop(0)
    time += 1
    if truck_weights:
        if sum(q) + truck_weights[0] <= weight:
            q.append(truck_weights.pop(0))
        else:
            q.append(0)

```

리스트의 0번 인덱스가 1개 빠질 떄마다 1초 증가한다. 빠진 자리에는 **트럭이 추가되거나 0이 추가된다**.

1. 트럭이 추가되는 경우
다리 위의 무게(`sum(q) + truck_weights[0]`)가 최대 무게(`weight`)보다 가볍거나 같다.
2. 0이 추가되는 경우
다리 위의 무게(`sum(q) + truck_weights[0]`)가 최대 무게(`weight`)보다 무겁다.

만약 `weight = 10`, `bridge_length = 2`, `truck_weights = [7,4,5,6]` 인 경우에 `트럭[7]`이 지나갈 때까지 다음 트럭이 리스트 안에 들어갈 수 없다

```python
0 0 (time = 0)
0 7 (1s)
7 0 (2s)
0 4 (3s)
4 5 (4s)
5 0 (5s)
0 6 (6s)
6   (7s)
    (8s)
break
```

**append와 pop을 쓰는 문제.** 센스가 중요한 문제같다.

# 문제6. 주식가격
![](https://velog.velcdn.com/images/miracle-21/post/f054bf57-1bdb-4124-93fb-028120a85a2c/image.png)
```py
from collections import deque

def solution(prices):
    q = deque(prices)
    answer = []
    while q:
        price = q.popleft()
        sec = 0
        for i in q:
            sec += 1
            if price > i:
                break
        answer.append(sec)
    return answer
```

간단한거같은데 왜 못푼건지 모르겠다.

**deque를 이용한 문제.**

# 문제7. 두 큐 합 같게 만들기
![](https://velog.velcdn.com/images/miracle-21/post/04d90af2-77d7-43e3-98fa-f83c00e5ecfa/image.png)

```py
from collections import deque

def solution(queue1, queue2):
    q1 = deque(queue1)
    q2 = deque(queue2)
    sum1 = sum(q1)
    sum2 = sum(q2)
    avr = (sum1+sum2)/2
    result = 0
    while sum1 != sum2 != avr:
        if len(q1) == 0 or len(q2) == 0 or result > 3000000:
            return -1
        elif sum1 > sum2:
            a = q1.popleft()
            q2.append(a)
            sum1 -= a
            sum2 += a
            result += 1
        elif sum1 < sum2:
            a = q2.popleft()
            q1.append(a)
            sum2 -= a
            sum1 += a
            result += 1
    return result
```
처음에는 if문 마다 q1과 q2의 합 중 큰값을 구하는 식으로 했는데 시간초과가 나서 `sum1`, `sum2` 변수를 따로 만들었다.

그래도 11번, 28번에서 시간초과가 나서 질문하기를 보니 무한루프가 돌 수 있다고 해서, 30만번을 초과하면 -1이 리턴되도록 수정하니 통과했다.

**deque를 이용한 문제.**

---
<이론 출처>
https://freedeveloper.tistory.com/370
