## 구조

- 배열은 순차적으로 연결된 공간에 데이터를 나열하는 데이터 구조
    - 단점은 연결된 공간이 준비돼있어야한다는 점, 데이터 저장공간이 떨어지는 순간 배열의 역할을 할 수 없음
- 이런 배열의 단점을 커버하기 위해서 사용하는 것이 링크드 리스트
- 떨어진 곳에 존재하는 데이터를 화살표로 연결해서 관리하는 데이터 구조가 링크드 리스트

## 용어

- 노드: 데이터 저장단위 (데이터값 + 포인터)
- 포인터: 각 노드 안에서 다음/이전 노드와의 연결 정보를 가지고 있는 공간

> - 맨 앞에 있는 노드의 주소만 알 수 있으면 전체 데이터에 접근이 가능
- 마지막 데이터의 경우, 그 다음에 연결되는 노드가 없기 때문에 포인터의 값이 null임
> 

## 장단점

### 장점

- 미리 데이터 공간을 할당하지 않아도 됨

### 단점

- 연결을 위한 별도의 데이터 공간이 필요함(포인터를 저장할 공간) → 저장 공간 효율이 높지 않음
- 연결 정보를 찾는 시간이 필요하므로 접근 속도가 느림
- 중간 데이터를 삭제하는 경우, 앞 뒤 데이터의 연결을 재구성해야하는 부가적인 작업이 필요

## 구현

> Node에는 데이터값 그리고 포인터, 이렇게 두 가지의 정보가 들어가기 때문에 Class를 활용하여 구현하는 편임
> 
- Node 구현

```python
class Node:
	def __init__ (self, data):
		self.data = data
		self.next = None
```

```python
class Node:
	def __init__ (self, data, next=None):
		self.data = data
		self.next = next
```

- Node와 Node 연결 (포인터 활용)

```python
node1 = Node(1)
node2 = Node(2)
```

```python
node1.next = node2
head = node1
```

- 데이터 추가하기

```python
class Node:
	def __init__ (self, data, next=None):
		self.data = data
		self.next = next

	def add(data):
		node = head
		while node.next:
			node = node.next
		node.next = Node(data)
```

- 링크드 리스트 데이터 출력하기(검색)

```python
node = head
while node.next:
	print(node.data)
	node = node.next
print(node.data)
```

- 중간에 데이터 삽입
    1. 삽입하고자 하는 포인터를 찾음(원하는 데이터를 가진 node 찾기)
    2. 기존 node의 포인터가 새로운 node를 가리키게 하고
    3. 새로운 node의 포인터가 찾은 node.next를 가리키게 해야함

```python
# 1과 2 사이에 해당 노드를 추가하고자 함
node3 = node(1.5)

search = True
node = head
while search:
	if node.data == 1:
		search = false
	else:
		node = node.next

node_next = node.next
node.next = node3
node3.next = node_next
```

- 중간에 데이터 삭제
    1. head 노드를 삭제하는 경우
        1. head의 값을 임시 변수에 옮겨두고 head를 [head.next](http://head.next) 값으로 변경하고 임시 변수 삭제
    2. 중간 노드 혹은 마지막 노드 삭제하는 경우
        1. 삭제하려는 노드 이전에 연결된 노드를 찾음
        2. 삭제하려는 노드를 임시 변수에 옮김
        3. 삭제하려는 노드 이전의 노드의 next를 삭제하려는 노드의 next와 연결 그리고 임시변수 삭제

```python
# data를 가진 node를 삭제해라
def delete(self, data):
	# node가 아예 없는 경우
	if self.head == '':
		print("해당 값을 가진 노드가 없습니다")
		return
	
	# head를 삭제하는 경우
	if self.head.data == data:
		temp = self.head
		self.head = self.head.next
		del temp
	else:
		# 삭제하고자 하는 node를 검색하는 과정
		node = self.head
		while node.next:
			# 삭제하려는 노드 이전에 연결된 노드를 찾아야하기 때문에 node.data가 아닌 node.next.data를 기준으로 검색
			if node.next.data == data:
				temp = node.next
				node.next = node.next.next
				del temp
				return
			else:
				node = node.next

```