## 힙이란

데이터에서 최대값과 최소값을 빠르게 찾기 위해 고안된 완전 이진트리

## 사용하는 이유

- 배열에서 최대/최소값 찾는 시간 복잡도: O(n) (모든 데이터를 검색해야하기 때문에)
- 힙에서 최대/최소값을 찾는 시간 복잡도: O(logn)

## 구조

- 최대값을 구하기 위한 최대힙(Max Heap)과 최소값을 구하기 위한 최소힙(Min Heap)으로 나뉨
- 각 노드의 값은 해당 노드의 자식 노드의 값보다 크거나 같다(최대 힙의 경우) (힙의 구조를 갖추면 항상 데이터를 가장 위에 있는 루트 노드를 가져오면 됨)
- 완전 이진 트리의 형태를 가짐(데이터를 넣을 때 항상 왼쪽부터 채워나가고 이진 트리라서 자식은 두개씩)
- 이진탐색트리 vs 힙: 이진탐색트리는 탐색을 위한 구조, 힙은 최대/최소값을 위한 구조

## 구현

- 힙을 배열로 표현
    - 루트 노드 index는 편의상 1로 설정
    - 부모 노드 인덱스 = 자식 노드 // 2
    - 왼쪽 자식 노드 인덱스 = 부모 * 2
    - 오른쪽 자식 노드 인덱스 = 부모 * 2 + 1
- 데이터 넣기
    - max heap의 경우, 루트노드보다 삽입할 데이터가 더 클 경우
    1. 일단 완전 이진 트리 구조에 맞춰서 데이터 삽입
    2. 자식 노드와 부모 노드의 크기 비교 → 자식 노드가 더 클 경우 swap → 반복
- 데이터 삭제
    1. 루트 노드에 있는 값을 꺼냄
    2. 가장 마지막에 들어갔던 데이터를 루트 노드로 올림
    3. 루트노드가 자식 노드보다 작을 경우, 자식 노드 중 더 큰 값과 루트 노드를 바꿈(힙 재구성)

```python
class Heap:
    def __init__(self, data):
        self.heap_array = list()
        self.heap_array.append(None)
        self.heap_array.append(data)
    
    #새로 들어온 값과 그 부모 노드를 비교해서 바꿔야하는지 여부를 체크
    def move_up(self, inserted_idx):
        #idx가 1이라면 루트 노드이기 때문에 바꿀 필요x
        if inserted_idx <= 1:
            return False
        
        parent_idx = inserted_idx // 2
        if self.heap_array[inserted_idx] > self.heap_array[parent_idx]:
            return True
        else:
            return False
        
    def insert(self, data):
        if len(self.heap_array) == 0:
            self.heap_array.append(None)
            self.heap_array.append(data)
            retrun True
            
        self.heap_array.append(data)
        
        inserted_idx = len(self.heap_array) - 1
        
        while self.move_up(inserted_idx):
            parent_idx = inserted_idx // 2
            self.heap_Array[inserted_idx], self.heap_array[parent_idx] = self.heap_array[parent_idx], self.heap_Array[inserted_idx]
            inserted_idx = parent_idx
        
        return True
```

```python
#루트 노드를 다시 채워가면서 힙의 구조 만들어가기
def move_down(self, popped_idx):
    left_child_popped_idx = popped_idx * 2
    right_child_popped_idx = popped_idx * 2 + 1
    
    #case1: 왼쪽 자식 노드도 없을 때 -> 이진트리이기 때문에 왼쪽 노드 없으면 오른쪽도 없음
    if left_child_popped_idx >= len(self.heap_array):
        return False
    #case2: 오른쪽 자식 노드만 없을 때
    elif right_child_popped_idx >= len(self.heap_array):
        if self.heap_array[popped_idx] < self.heap_array[left_child_popped_idx]:
            return True
        else:
            return False
    #case3: 왼쪽, 오른쪽 자식 노드 모두 있을 때
    else:
        if self.heap_array[left_child_popped_idx] > self.heap_array[right_child_popped_idx]:
            if self.heap_array[popped_idx] < self.heap_array[left_child_popped_idx]:
                return True
            else:
                return False
        else:
            if self.heap_array[popped_idx] < self.heap_array[right_child_popped_idx]:
                return True
            else:
                return False

#루트 노드 삭제하기
def pop(self):
    if len(self.heap_array)<= 1:
        return None
    
    returned_data = self.heap_array[1] # 루트 노드 값 저장
    self.heap_array[1] = self.heap_array[-1] # 마지막 노드값 루트 노드로 이동
    del self.heap_array[-1] # 마지막 노드 삭제
    popped_idx = 1
    
    while self.move_down(popped_idx):
        left_child_popped_idx = popped_idx * 2
        right_child_popped_idx = popped_idx * 2 + 1

        #case1: 왼쪽 자식 노드도 없을 때
        if left_child_popped_idx >= len(self.heap_array):
            return False
        #case2: 오른쪽 자식 노드만 없을 때
        elif right_child_popped_idx >= len(self.heap_array):
            if self.heap_array[popped_idx] < self.heap_array[left_child_popped_idx]:
                self.heap_array[popped_idx], self.heap_array[left_child_popped_idx] = self.heap_array[left_child_popped_idx], self.heap_array[popped_idx]
                popped_idx = left_child_popped_idx
            else:
                return False
        #case3: 왼쪽, 오른쪽 자식 노드 모두 있을 때
        else:
            if self.heap_array[left_child_popped_idx] > self.heap_array[right_child_popped_idx]:
                if self.heap_array[popped_idx] < self.heap_array[left_child_popped_idx]:
                    self.heap_array[popped_idx], self.heap_array[left_child_popped_idx] = self.heap_array[left_child_popped_idx], self.heap_array[popped_idx]
                popped_idx = left_child_popped_idx
                else:
                    return False
            else:
                if self.heap_array[popped_idx] < self.heap_array[right_child_popped_idx]:
                    self.heap_array[popped_idx], self.heap_array[right_child_popped_idx] = self.heap_array[right_child_popped_idx], self.heap_array[popped_idx]
                popped_idx = right_child_popped_idx
                else:
                    return False
    
        return returned_data
```