- O(nlogn)
- stable sort

요소를 쪼갠 후 다시 합병하면서 정렬해나가는 방식 (재귀 용법 활용)

1. 리스트를 절반으로 잘라 비슷한 크기의 두 부분 리스트로 나눔
2. 각 부분 리스트를 재귀적으로 합병 정렬을 이용해 정렬함
3. 두 부분 리스트를 다시 하나의 리스트로 합침

→ 재귀 용법으로 리스트를 나누는 함수(split, 데이터의 길이가 1일때까지 나눔), 나눠진 함수를 비교해서 합치는 함수(merge) 필요

```python
[ 7 3 1 5 6 4 2 ]
[ 7 3 1 | 5 6 4 2 ]
[ 7 | 3 1 | 5 6 | 4 2 ]
[ 7 | 3 | 1 | 5 | 6 | 4 | 2 ]
```

- 이 쪼개진 배열들을 다시 합치면서 정렬하는 것이 merge sort

```python
[ 7 | 1 3 | 5 6 | 2 4 ]
[ 1 3 7 | 2 4 5 6 ]
# -> 이때 합치는 방법
# 앞 뒤 배열에 포인터를 하나씩 두고 비교, 작은거 기입, 기입하면 포인터 +1
[ 1 2 3 4 5 6 7 ]
```

- O(n)이 필요한 과정을 logn번 반복 = O(nlogn)

```python
def merge(left, right):
    merged = list()
    left_point, right_point = 0,0 #각각의 index번호

    #case1: left/right 아직 남아있을 때
    while len(left) > left_point and len(right) > right_point:
        if left[left_point] > right[right_point]:
            merged.append(right[right_point])
            right_point += 1
        else:
            merged.append(left[left_point])
            left_point += 1
    #case2: left만 남아있을 때
    while len(left) > left_point:
        merged.append(left[left_point])
        left_point += 1
    #case3: right만 남아있을 때
    while len(right) > right_point:
        merged.append(right[right_point])
        right_point += 1

    return merged

def mergesplit(data):
    if len(data) <= 1:
        return data
    medium = int(len(data)/2)
    left = mergesplit(data[:medium])
    right = mergesplit(data[medium:])

    return merge(left, right)

import random

data_list = random.sample(range(100),10)
print(data_list)
mergesplit(data_list)
```