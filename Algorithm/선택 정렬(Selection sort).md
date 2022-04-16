# 선택 정렬(Selection sort)

## **선택 정렬 (Selection Sort)**

Selection Sort는 Bubble Sort과 유사한 알고리즘으로, **해당 순서에 원소를 넣을 위치는 이미 정해져 있고, 어떤 원소를 넣을지 선택하는 알고리즘**입니다.

Selection Sort와 Insertion Sort를 헷갈려하시는 분들이 종종 있는데, Selection Sort는 배열에서 **해당 자리를 선택하고 그 자리에 오는 값을 찾는 것**이라고 생각하시면 편합니다.

## **Process (Ascending)**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d72cbb49-2f28-4c21-84b9-8b5e87d90565/Untitled.png)

- 1회전:
첫 번째 자료 9를 두 번째 자료부터 마지막 자료까지와 비교하여 가장 작은 값을 첫 번째 위치에 옮겨 놓는다. 이 과정에서 자료를 4번 비교한다. ⇒ n-1 번
- 2회전:
두 번째 자료 6을 세 번째 자료부터 마지막 자료까지와 비교하여 가장 작은 값을 두 번째 위치에 옮겨 놓는다. 이 과정에서 자료를 3번 비교한다. ⇒ n-2 번
- 3회전:
세 번째 자료 7을 네 번째 자료부터 마지막 자료까지와 비교하여 가장 작은 값을 세 번째 위치에 옮겨 놓는다. 이 과정에서 자료를 2번 비교한다. ⇒ n-3 번 ...
- 4회전:
네 번째 자료 9와 마지막에 있는 7을 비교하여 서로 교환한다. ⇒ 1번

## C++ **Code (Ascending)**

```cpp
#include<iostream>
#include<algorithm>
using namespace std;

int arr[8] = {8, 6, 5, 3, 1, 2, 7, 4};
int main(){
	for(int i =0 ; i<8 ; i++){
		int minn = arr[i];
		int loc = i;
		for(int j = i+1 ; i<8 ; j++){
			if(minn > arr[j]){
				minn = arr[j];
				loc = j;
				}
			}
		swap(arr[i], arr[loc]);
	}

}
```

1. 우선, 위치(index)를 **선택**해줍니다.
2. i+1번째 원소부터 선택한 위치(index)의 값과 비교를 시작합니다.
3. 오름차순이므로 현재 선택한 자리에 있는 값보다 순회하고 있는 값이 작다면, 위치(index)를 갱신해줍니다.
4. '2'번 반복문이 끝난 뒤에는 indexMin에 '1'번에서 선택한 위치(index)에 들어가야하는 값의 위치(index)를 갖고 있으므로 서로 교환(swap)해줍니다.

## **GIF로 이해하는 Selection Sort**

![https://github.com/GimunLee/tech-refrigerator/raw/master/Algorithm/resources/selection-sort-001.gif](https://github.com/GimunLee/tech-refrigerator/raw/master/Algorithm/resources/selection-sort-001.gif)

## **시간복잡도**

데이터의 개수가 n개라고 했을 때,

- 첫 번째 회전에서의 비교횟수 : 1 ~ (n-1) => n-1
- 두 번째 회전에서의 비교횟수 : 2 ~ (n-1) => n-2
    
    ...
    
- `(n-1) + (n-2) + .... + 2 + 1 => n(n-1)/2`

비교하는 것이 상수 시간에 이루어진다는 가정 아래, n개의 주어진 배열을 정렬하는데 O(n^2) 만큼의 시간이 걸립니다. 최선, 평균, 최악의 경우 시간복잡도는 **O(n^2)** 으로 동일합니다.

## **공간복잡도**

주어진 배열 안에서 교환(swap)을 통해, 정렬이 수행되므로 **O(n)** 입니다.

## **장점**

- Bubble sort와 마찬가지로 알고리즘이 단순합니다.
- 정렬을 위한 비교 횟수는 많지만, Bubble Sort에 비해 실제로 교환하는 횟수는 적기 때문에 많은 교환이 일어나야 하는 자료상태에서 비교적 효율적입니다.
- Bubble Sort와 마찬가지로 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않습니다. => 제자리 정렬(in-place sorting)

## **단점**

- 시간복잡도가 O(n^2)으로, 비효율적입니다.
