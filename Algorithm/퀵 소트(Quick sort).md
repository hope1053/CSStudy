# 퀵 소트(Quick sort)

> 특정한 값(pivot)값을 기준으로 큰 숫자는 오른쪽, 작은 숫자는 왼쪽으로 구분하자!
> 

분할 정복 알고리즘으로 평균 속도가 O(N*logN)이다.

### **퀵소트**

![Untitled - 2022-04-16T213459 187](https://user-images.githubusercontent.com/71035113/163675193-f194548f-bdfc-4a35-bbce-eb2afbc291e5.png)
![Untitled - 2022-04-16T213502 349](https://user-images.githubusercontent.com/71035113/163675196-7e11c96c-7112-4419-962b-7c0d4d88ee1a.png)
![Untitled - 2022-04-16T213505 374](https://user-images.githubusercontent.com/71035113/163675198-d5896e07-a58a-4a03-bb20-15357430ed62.png)

---

```cpp
#include <iostream>
#include <vector>

using namespace std;

void quickSort(int *data, int start, int end) {
  if (start >= end) return;
  int pivot = start;  // 기준 값
  int i = start + 1;
  int j = end;

  while (i <= j) {
    while (data[i] <= data[pivot])  // 키 값보다 큰 값 만날때까지 오른쪽으로 이동
      i++;
    while (data[j] >= data[pivot] && j > start)  // 키 값보다 작은 값 만날 때까지 왼쪽으로 이동
      j--;
    if (i > j)  //현재 엇갈린 상태면 pivot 값 교체
    {
      int temp = data[j]; // j와 pivot 교체
      data[j] = data[pivot];
      data[pivot] = temp;
    } else {
      int temp = data[j]; // j와 i 교체
      data[j] = data[i];
      data[i] = temp;
    }
    // 재귀 호출 - 이제 교환된 피벗 기준으로 왼쪽엔 피벗보다 작은 값, 오른쪽엔 큰 값들만 존재함
    quickSort(data, start, j - 1);
    quickSort(data, j + 1, end);
  }
}

int main() {
  int data[7] = {38,27,43,9,3,82,10};
  int len = 7;
  quickSort(data, 0, len - 1);

  for (int i = 0; i < len; i++) cout << data[i] << ' ';

  return 0;
}
```

### **시간복잡도**

- 퀵 정렬에서 대부분의 시간을 차지하는 것은 수열을 pivot 값을 기준으로 부분 수열로 나누는 과정입니다.퀵정렬의 경우 나눠지는 두 부분 수열이 비슷한 크기로 나눠진다고 보장할 수 없습니다.
- 만약 기준 값이 수열의 최소 또는 최대값일 경우 부분 수열의 크기가 1씩만 줄어드는 현상이 발생하므로, 이런 최악의 경우 시간복잡도는 `O(N^2)`이 됩니다.
- 하지만 평균적으로 부분 문제가 절반에 가깝게 나눠질 경우 시간복잡도는 `O(nlgn)`이 됩니다.그래서 퀵정렬에는 가능한 한 절반에 가까운 분할을 얻기 위해 좋은 pivot 값을 뽑는 다양한 방법들을 사용합니다.
- 정리하면 퀵정렬은 `중간에 가까운 pivot을 선택하는 방법`을 적용하기 때문에 평균적으로 빠른 속도를 낼 수 있고, 시간복잡도는 `O(nlgn)` 입니다.
- 심지어 퀵정렬은 같은 big O를 갖는 다른 정렬 알고리즘에 비해 빠른 속도를 보입니다. 그 이유는 데이터의 이동이 데이터의 비교에 비해 현저히 적게 일어나고, 병합정렬처럼 별도의 메모리 공간이 필요하지 않기 때문이라고 합니다.
