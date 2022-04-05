## 아이디어

- 리스트를 두 개의 서브 리스트로 나눔
- 중간값과 검색할 숫자를 비교하여 다시 검색할 리스트를 고름 → 반복
- 탐색 대상이 되는 리스트는 정렬돼있다고 가정

## 구현

```python
def binary_search(data, search):
    if len(data) == 1 and search == data[0]:
        return True
    if len(data) == 1 and search != data[0]:
        return False
    if len(data) == 0:
        return False
        
    medium = len(data) // 2
    if search == data[medium]:
        return True
    else:
        if search > data[medium]:
            return binary_search(data[medium:], search)
        else:
            return binary_search(data[:medium], search)

import random
data_list = random.sample(range(100), 10)
data_list.sort()
print(data_list)
print(binary_search(data_list, 75))
```

```python
def binary_search(data, search):
	left, right = 0, len(data) - 1

	while left < right:
		pivot = (left + right) // 2

		if data[pivot] < search:
				left = pivot + 1
		elif data[pivot] > search:
				right = pivot - 1
		else:
				return pivot

	return False
```

## 시간 복잡도

- n개의 리스트를 2로 나누어 길이가 1이 될 때까지 비교 연산을 k회 진행
- n x 1/2 x 1/2 ... = 1
- n x (1/2)^k = 1
- n = 2^k = log2n = log2 2^k
- log 2n = k
- Big(O) 표기법으로는 k + 1이 결국 최종 시간 복잡도임
- 결국 O(log2 n +1)이고 → O(logn)