- O(nlogn)
- unstable sort

(완전 이진 트리)힙 자료구조를 기반으로 한 정렬 방식

- Max Heap의 경우, Heap을 pop하면 max값
- array의 맨 뒤로 보냄 → 다시 Heap정렬
- max찾는 O(n) + max값을 array의 맨 뒤로 보내는 O(logn) * n번 진행 = O(nlogn)

```python
from typing import List
import heapq

#in place memory sorting
def heapSort(nums:List[int])->List[int]:
  #python does not have maxHeap. multiply by -1
  nums = [-1*n for n in nums]
  # nums = [-3, -5, -7, -9, -4, -2]
  heapq.heapify(nums)

  sorted = [0] * len(nums)
  
  for i in range(len(nums)-1,-1,-1):
    largest = -1 * heapq.heappop(nums)
    sorted[i] = largest
  return sorted

print(heapSort(nums=[3, 5, 7, 9, 4, 2]))
# [2, 3, 4, 5, 7, 9]
```