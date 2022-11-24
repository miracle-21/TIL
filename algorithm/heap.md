- [힙 정렬](#힙-정렬)
- [힙 큐 알고리즘](#힙-큐-알고리즘)
- [문제1. 더 맵게](#문제1-더-맵게)

#

**⭐⭐⭐ import heapq**

#

# 힙 정렬

- 최대값 및 최소값을 찾아내기 위한 완전이진트리의 자료구조
- 부모 노드의 두 자식 중 더 큰 자식과 자신의 위치를 바꾸는 알고리즘
- **우선순위**를 구현하기 위해 사용하는 자료구조다.

# 힙 큐 알고리즘

- heapq.**heappush**(*heap*, *item*): *item* 값을 *heap*으로 푸시
- heapq.**heappop**(*heap*): *heap*에서 가장 작은 항목을 팝하고 반환
- heapq.**heappushpop**(*heap*, *item*): 힙에 *item*을 푸시한 다음, *heap*에서 가장 작은 항목을 팝하고 반환
- heapq.**heapify**(*x*): 리스트 *x*를 선형 시간으로 제자리에서 힙으로 변환
- heapq.**heapreplace**(*heap*, *item*): *heap*에서 가장 작은 항목을 팝하고 반환하며, 새로운 *item*도 푸시
- heapq.**merge**(**iterables*, *key=None*, *reverse=False*) :여러 정렬된 입력을 단일 정렬된 출력으로 병합
- heapq.**nlargest**(*n*, *iterable*, *key=None*): *iterable*에 의해 정의된 데이터 집합에서 *n* 개의 가장 큰 요소로 구성된 리스트를 반환
- heapq.**nsmallest**(*n*, *iterable*, *key=None*): *iterable*에 의해 정의된 데이터 집합에서 *n* 개의 가장 작은 요소로 구성된 리스트를 반환
    
    출처: [https://docs.python.org/ko/3/library/heapq.html](https://docs.python.org/ko/3/library/heapq.html)
    

# 문제1. 더 맵게

![스크린샷, 2022-11-24 12-33-35.png](%E1%84%92%E1%85%B5%E1%86%B8%20f1cf4555f43b497aa1e28e057b5b9f17/%25EC%258A%25A4%25ED%2581%25AC%25EB%25A6%25B0%25EC%2583%25B7_2022-11-24_12-33-35.png)

```jsx
import heapq

def solution(scoville, K):
    heap = scoville
    heapq.heapify(heap)
    answer = 0
    try:
        while heap[0] < K:
            heapq.heappush(heap, heapq.heappop(heap) + (heapq.heappop(heap) * 2))
            answer += 1
        return answer
    except:
        return -1
```

처음에는 deque를 사용했다가, `가장 맵지 않은 음식 + (두 번째로 매운 음식 * 2)`의 값이 list의 최솟값이 아닐 수 있다는 힌트를 얻었다. heapq는 가장 작은 수를 앞으로 자동으로 정렬시켜주기 때문에 사용법을 확인하고 재시도하니 바로 성공.

**heapq를 사용한 문제.**