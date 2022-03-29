```python
[391, 582, 50, 924, 134, 8, 192]
```

- counting sort: 900개 이상의 공간이 필요함
- radix sort: 자리수 별로 정리(1의 자리수 별로)
    - 무조건 stable해야함
    - 0~9까지 제한됨
- 1의 자리수를 기준으로 정렬함 : [50, 391, 582, 192, 924, 134, 08]
- 10의 자리수를 기준으로 정렬함 : [08, 924, 134, 50, 582, 391, 192]
- 100의 자리수를 기준으로 정렬함 : [ 8, 50, 134, 192, 392, 582, 924]
- O(n+k) (각 자리수별로 정렬할때 counting sort하는 시간 복잡도) x w(자리수)
    - 이때 k는 각 자리 수에 존재하는 수의 갯수 = 10으로 고정 (나올 수 있는 값의 범위가 0~9이기 때문에)
    - w는 자리수 (100단위 = 3)

→ O(w(n+k))

```python
from typing import List
import math

def countingSortByDigit(nums:List[int],digit:int)->List[int]:  
  counts = [0]*10
  for num in nums:
    count_idx = num//pow(10,digit)%10
    counts[count_idx] += 1

  acc_counts = []
  acc_count = 0
  for count in counts:
    acc_count += count
    acc_counts.append(acc_count)
  end_locs = [ c-1 for c in acc_counts]

  sorted = [0] * len(nums)
  for num in reversed(nums):
    count_idx = num//pow(10,digit)%10
    end_loc = end_locs[count_idx]
    sorted[end_loc] = num
    end_locs[count_idx] -= 1

  return sorted

def radixSort(nums:List[int])->List[int]:
  largest_num = max(nums)
  digits = int(math.log10(largest_num))+1
  sorted = nums
  for digit in range(digits):
    sorted = countingSortByDigit(nums=sorted,digit=digit)
  return sorted

print(radixSort(nums=[391,582,50,924,8,192]))
```