# **삽입 정렬 (Insertion Sort)**

손 안의 카드를 정렬하는 방법과 유사합니다.

Insertion Sort는 Selection Sort와 유사하지만, 좀 더 효율적인 정렬 알고리즘입니다.

Insertion Sort는 **2번째 원소부터 시작하여 그 앞(왼쪽)의 원소들과 비교하여 삽입할 위치를 지정한 후, 원소를 뒤로 옮기고 지정된 자리에 자료를 삽입** 하여 정렬하는 알고리즘입니다.

최선의 경우 O(N)이라는 엄청나게 빠른 효율성을 가지고 있어, 다른 정렬 알고리즘의 일부로 사용될 만큼 좋은 정렬 알고리즘입니다.

<aside>
💡 현재 key 값이 앞에서 들어갈 자리를 찾는 것

</aside>

## **Process (Ascending)**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6a5f79be-25a0-400c-b5d7-20d5c4b86094/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e41f8622-c969-4ef7-85a7-b41cb85f0f04/Untitled.png)

## C **Code (Ascending)**

```cpp
# include <stdio.h>
# define MAX_SIZE 5

// 삽입 정렬
void insertion_sort(int list[], int n){
  int i, j, key;

  // 인텍스 0은 이미 정렬된 것으로 볼 수 있다.
  for(i=1; i<n; i++){
    key = list[i]; // 현재 삽입될 숫자인 i번째 정수를 key 변수로 복사

    // 현재 정렬된 배열은 i-1까지이므로 i-1번째부터 역순으로 조사한다.
    // j 값은 음수가 아니어야 되고
    // key 값보다 정렬된 배열에 있는 값이 크면 j번째를 j+1번째로 이동
    for(j=i-1; j>=0 && list[j]>key; j--){
      list[j+1] = list[j]; // 레코드의 오른쪽으로 이동
    }

    list[j+1] = key;
  }
}

void main(){
  int i;
  int n = MAX_SIZE;
  int list[n] = {8, 5, 6, 2, 4};

  // 삽입 정렬 수행
  insertion_sort(list, n);

  // 정렬 결과 출력
  for(i=0; i<n; i++){
    printf("%d\n", list[i]);
  }
}
```

1. 첫 번째 원소 앞(왼쪽)에는 어떤 원소도 갖고 있지 않기 때문에, 두 번째 위치(index)부터 탐색을 시작합니다. temp에 임시로 해당 위치(index) 값을 저장하고, prev에는 해당 위치(index)의 이전 위치(index)를 저장합니다.
2. 이전 위치(index)를 가리키는 prev가 음수가 되지 않고, 이전 위치(index)의 값이 '1'번에서 선택한 값보다 크다면, 서로 값을 교환해주고 prev를 더 이전 위치(index)를 가리키도록 합니다.
3. '2'번에서 반복문이 끝나고 난 뒤, prev에는 현재 **temp 값보다 작은 값들 중 제일 큰 값의 위치(index)** 를 가리키게 됩니다. 따라서, (prev+1)에 temp 값을 삽입해줍니다.

## **GIF로 이해하는 Insertion Sort**

![https://github.com/GimunLee/tech-refrigerator/raw/master/Algorithm/resources/insertion-sort-001.gif](https://github.com/GimunLee/tech-refrigerator/raw/master/Algorithm/resources/insertion-sort-001.gif)

## **시간복잡도**

최악의 경우(역으로 정렬되어 있을 경우) Selection Sort와 마찬가지로, `(n-1) + (n-2) + .... + 2 + 1 => n(n-1)/2` 즉, **O(n^2)** 입니다.

하지만, 모두 정렬이 되어있는 경우(Optimal)한 경우, 한번씩 밖에 비교를 안하므로 **O(n)** 의 시간복잡도를 가지게 됩니다. 또한, 이미 정렬되어 있는 배열에 자료를 하나씩 삽입/제거하는 경우에는, 현실적으로 최고의 정렬 알고리즘이 되는데, 탐색을 제외한 오버헤드가 매우 적기 때문입니다.

최선의 경우는 **O(n)** 의 시간복잡도를 갖고, 평균과 최악의 경우 **O(n^2)** 의 시간복잡도를 갖게 됩니다.

## **공간복잡도**

주어진 배열 안에서 교환(swap)을 통해, 정렬이 수행되므로 **O(n)** 입니다.

## **장점**

- 알고리즘이 단순합니다.
- 대부분의 원소가 이미 정렬되어 있는 경우, 매우 효율적일 수 있습니다.
- 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않습니다. => 제자리 정렬(in-place sorting)
- Selection Sort나 Bubble Sort과 같은 O(n^2) 알고리즘에 비교하여 상대적으로 빠릅니다.

## **단점**

- 평균과 최악의 시간복잡도가 O(n^2)으로 비효율적입니다.
- Bubble Sort와 Selection Sort와 마찬가지로, 배열의 길이가 길어질수록 비효율적입니다.
