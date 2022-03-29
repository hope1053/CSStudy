- O(n+k) (k는 array의 길이) 가장 큰수 - 가장 작은수
- stable sort

주어진 배열을 counting해서 정렬

```python
[3,4,0,1,2]
# 가장 작은 수 0 가장 큰 수 4 -> len 5의 array생성
[1,1,1,1,1] (count array)
[1,2,3,4,5] (누적 카운트)
[0,1,2,3,4]
```

- 누적 카운트가 각 숫자의 끝 위치 정보를 갖고 있음
    - 각 숫자가 몇번째 index에서 끝내는지 알아내기 위해 누적 카운트

```python
[3,2,5,1,2,5]
```

- count: [0,0,0,0,0] → [1, 2, 1, 0, 2] → [1, 3, 4, 4, 6]
- [1, 2, 2, 3, 5, 5]

```python
from typing import List

def countingSort(nums:List[int])->List[int]:  
  length = len(nums)
  min_num = min(nums)  #offset
  max_num = max(nums)

  range = max_num - min_num + 1
  counts = [0]*range

  for num in nums:
    count_idx = num - min_num
    counts[count_idx] += 1

  acc_counts = []
  acc_count = 0
  for count in counts:
    acc_count += count
    acc_counts.append(acc_count)

	# [ 0, 2, 3, 3, 5 ]
  end_locs = [ c-1 for c in acc_counts]

  sorted = [0] * length
  for num in reversed(nums):
    count_idx = num - min_num
    end_loc = end_locs[count_idx]
    sorted[end_loc] = num
    end_locs[count_idx] -= 1

  return sorted

print(countingSort(nums=[3,4,0,1,2]))
print(countingSort(nums=[3,0,5,1,0,5]))

# [0, 1, 2, 3, 4]
# [0, 0, 1, 3, 5, 5]
```

```python
# counting sort 구현
def counting_sort(array, max):
 
    #counting array 생성
    counting_array = [0]*(max+1)
 
    #counting array에 input array내 원소의 빈도수 담기
    for i in array:
        counting_array[i] += 1
 
    #counting array 업데이트.
    for i in range(max):
        counting_array[i+1] += counting_array[i]
 
    #output array 생성
    output_array = [-1]*len(array)
 
    #output array에 정렬하기(counting array를 참조)
    for i in array:
        output_array[counting_array[i] -1] = i
        counting_array[i] -= 1
    return output_array
```