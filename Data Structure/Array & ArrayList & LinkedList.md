## ArrayList

- 자바에서 많이 사용되며 배열과의 가장 큰 차이점은 배열은 크기가 고정인 반면 ArrayList는 크기가 가변적으로 변함
- 내부적으로 저장이 가능한 메모리 용량(Capacity), 현재 사용 중인 공간의 크기(Size)
- Capacity 이상을 저장하려고 할 때 더 큰 공간의 메모리를 새롭게 할당

## Array vs LinkedList vs ArrayList

> Array는 index로 값을 빠르게 찾을 수 있음
LinkedList는 데이터의 삽입 및 삭제가 빠름
ArrayList는 데이터를 찾는 것은 빠르지만 삽입 및 삭제가 느림
> 
- Array(배열)은 선언할 때 크기와 데이터 타입을 지정해야함
- 따라서 계속 데이터가 늘어나서 최대 사이즈를 알 수 없을 때는 사용하기에 부적합함 + 중간에 데이터를 삽입하거나 삭제하는 경우도..
- 하지만 index가 존재해서 검색이 편리함

- 이를 해결하기 위해서 List가 나옴
- 크기 정해줄 필요 없음, index도 있어서 검색도 빠름
- 중간에 데이터를 추가 및 삭제할 때 시간이 오래 걸림

- Linked List는 데이터 중간에 삽입 및 삭제를 하더라도 전체를 수정할 필요 없이 이전갑소가 다음값이 가르켰던 주소값만 수정해서 연결해주면 됨
- index가 없어서 검색하는 경우에는 순차적으로 처음부터 모두 살펴봐야해서 시간이 오래 걸림