# Stack

입력과 출력이 한 곳으로 제한된 자료구조

## 구조

- 가장 마지막에 넣은 데이터를 가장 먼저 접근해서 꺼낼 수 있음
- LIFO, FILO → 한쪽 끝에서만 자료를 넣거나 뺄 수 있음
- 보통 배열 구조를 활용해서 구현함
- 컴퓨터 내부의 프로세스 구조의 함수 동작 방식

## 동작

append, pop 활용

```python
data_stack = list()

data_stack.append(1)
data_stack.append(2)

data_stack.pop()
# 가장 마지막에 들어간 2가 나옴
```

# Queue

## 구조

- 가장 먼저 넣은 데이터를 가장 먼저 꺼낼 수 있음
- FIFO, LILO → 스택과는 꺼내는 순서가 반대
- 큐에 데이터를 넣는 기능: Enqueue
- 큐에서 데이터를 꺼내는 기능: Dequeue
- **멀티 태스킹을 위한 프로세스 스케쥴링 방식**을 구현하기 위해 많이 사용됨

## 동작

- 파이썬에서는 Queue(), LifoQueue(), PriorityQueue() 등 라이브러리를 활용해서 사용

```python
import queue

data_queue = queue.Queue()

data_queue.put(1)
data_queue.put(2)

data_queue.qsize()
# 2

data_queue.get()
# 1

```

### PriorityQueue

```python
import queue

data_queue = queue.PriorityQueue()

data_queue.put((10, "korea"))
data_queue.put((5, 1))
data_queue.put((15, "china"))

data_queue.get()
# (5,1) -> 우선순위가 가장 높은 것부터 뽑음
```

## 2개의 스택으로 큐 구현

- inBox, outBox 모두 stack
1. inBox에 데이터를 삽입(push)
2. inBox의 데이터를 모두 pop하여 outBox에 push
3. outBox의 데이터를 pop

```python
class MyQueue:
	def __init__(self):
		self.input = []
		self.output = []

	def push(self, x:int) -> None:
		self.input.append(x)

	def pop(self) -> int:
		self.peek()
		return self.output.pop()

	def peek(self) -> int:
		if not self.output:
			while self.input:
				self.output.append(self.input.pop())
		return self.output[-1]

	def empty(self) -> bool:
		return not self.input and not self.output
```