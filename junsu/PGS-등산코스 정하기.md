
# 2023-06-10 / 박준수 / PGS - 등산코스 정하기
# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->



# Approach
<!-- Describe your approach to solving the problem. -->


# Complexity
- Time complexity(First trial): $$O(nlog(n))$$

- Space complexity: $$O(n)$$


# Code

1. First Trial

```python
import heapq
from math import inf

def solution(n, paths, gates, summits):
    answer = [-1, inf]
    
    mountain =  [[] for _ in range(n + 1)]
    isSummit = [False] * (n + 1)
    distance = [inf] * (n + 1)
    
    for i,j,w in paths:
        mountain[i].append([j, w])
        mountain[j].append([i, w])
        
    for summit in summits:
        isSummit[summit] = True
            
    # print(mountain)
    # print(isSummit)
    
    queue = []
    for gate in gates:
        distance[gate] = 0
        heapq.heappush(queue, [0, gate])
        
    while queue:
        curr_dis, curr_des = heapq.heappop(queue)
        
        if distance[curr_des] < curr_dis or isSummit[curr_des]:
            continue
            
        for des, dis in mountain[curr_des]:
            dis = max(dis, distance[curr_des])
            if distance[des] > dis:
                distance[des] = dis
                heapq.heappush(queue, [dis, des])
    
        
    for summit in sorted(summits):
        if distance[summit] < answer[1]:
            answer[1] = distance[summit]
            answer[0] = summit
        
    
    return answer

```






