# 정규화(Normalization)

**Q. DB Normalization(정규화)란?**

A. 데이터베이스 정규화란 데이터의 중복을 줄이고 무결성을 향상시키는 등 여러 목적을 달성하기 위해 관계형 데이터베이스를 정규화된 형태로 재디자인 하는 것을 말한다. 

**Q. DB Normalization(정규화)의 목적은?**

A. 

- 불필요한 데이터를 제거하고 데이터의 중복을 최소화하기 위해서
- 데이터베이스 구조 확장할 때, 재디자인을 최소화하기 위해서
- 다양한 관점에서의 query를 지원하기 위해서

**Q. 정규화 과정?**

A. 정규화는 1정규화 ~ 6정규화 까지 있지만, 실무에서는 대체로 1~3 정규화까지의 과정을 거친다.

- 제 1정규화: 각 컬럼들은 값이 `원자값`을 가지게 바꾼다.
- 제 2정규화: 테이블의 모든 컬럼에서 `부분 함수 종속성`을 제거하는 것
- 제 3정규화: 기본키를 제외한 속성들 간의 `이행적 함수 종속성`을 없애는 것

**제 1정규화(First Normal Form, 1NF)**

테이블(Relation)이 제 1정규형을 만족했다는 것은 아래 `세 가지` 조건을 만족했다는 것을 의미한다. 

1. 어떤 Relation에 속한 모든 Domain(row)이 원자값(atomic value)만으로 되어 있다.
2. 모든 attribute에 반복되는 그룹이 나타나지 않는다.
3. 기본 키를 사용하여 관련 데이터의 각 집합을 고유하게 식별할 수 있어야 한다.

**예제)**

**1번 조건을 위반한 사례**

전화번호가 여러 개를 가지고 있고 이는 atomic하지 않으므로 제1정규형을 위반함

![Untitled (81)](https://user-images.githubusercontent.com/71035113/153178320-d0d93c53-adbd-4a17-a7f4-d1757007b40e.png)

**2번 조건을 위반한 사례**

전화번호 그룹이 반복되는 경우

따라서 재디자인 해야 함

![Untitled (82)](https://user-images.githubusercontent.com/71035113/153178327-b1d80c28-64d6-4ded-b90e-09085ec8f12f.png)

그런데 이렇게 바꾸게 되면, Relation ID가 더이상 고유하게 식별할 수 있는 키가 아니란 것을 확인할 수 있음 따라서, 3번 조건을 만족하기 위해 아래와 같이 테이블을 나누어 디자인하는 것이 좋다.

![Untitled (83)](https://user-images.githubusercontent.com/71035113/153178329-2dba379d-26bb-483d-936d-7f87ac11cbfe.png)

위 디자인은 Customer Name과 Customer Telephone Number가 One-to-Many 관계를 형성함

**제 2정규화(Second Normal Form, 2NF)**

제 2정규화를 수행 했을 경우 테이블의 **모든 컬럼이 `완전 함수적 종속`을 만족한다.**
(<=> 부분 함수적 종속이 모두 제거되었다.)

이를 이해하기 위해 부분 함수적 종속성과 완전 함수적 종속성이라는 용어를 알아야 한다.

- 함수적 종속: X값에 따라 Y값이 결정될 때 X→Y로 표현하는데 이를 Y는 X에 대해 `함수적 종속`이라고 한다. 예를 들어 학번을 알면 이름을 알 수 있는데 이 경우에 학번은 X가 되고 이름은 Y가 된다. X를 결정자라고 하고 Y를 종속자라고 한다. 다른 말로 X가 바뀌는 경우 Y가 바뀌어야만 한다는 것을 의미한다.
- 함수적 종속에서 X의 값이 여러 요소일 경우, {X1, X2} ⇒ Y일 경우 X1과 X2가 Y의 값을 결정할 때 이를 완전 함수적 종속이라고 하고 X1, X2 중 하나만 Y 값을 결정할 때 이를 부분 함수적 종속이라고 한다.

**예시**

![Untitled (84)](https://user-images.githubusercontent.com/71035113/153178331-fc757c15-aabb-41ad-ba52-266538b7e636.png)

위에서 Model과 Manufacturer를 알면 Model Full Name을 알 수 있기 때문에 {Model, Manufacturer} → Model Full Name이라고 할 수 있다. 

- Model Full name = Manufacturer + Model
    
    하지만 {Model, Manufacturer} → Manufacturer Country에서 Manufacturer Country는 Model아무 관계가 없기 때문에 Manufacturer Country는 Manufacturer와만 종속관계에 있게 되고 이를 부분 함수 종속이라고 하게 된다. 
    

![Untitled (85)](https://user-images.githubusercontent.com/71035113/153178335-ae113f3c-c9ea-4781-8fb1-8fcd7453154c.png)

부분 함수 종속을 제거한 이후의 테이블은 아래와 같고 이는 제2정규형을 만족한 테이블임

![Untitled (86)](https://user-images.githubusercontent.com/71035113/153178337-0adb405e-eb47-46cd-a419-16cdb090e986.png)

**제 3정규화(Third Normal Form, 3NF)**

테이블(Relation)이 제 3정규형을 만족한다는 것은 아래 두 가지 조건을 만족하는 것을 의미한다.

1. Relation이 제 2정규화 되었다. (The relation is in second normal form)
2. 기본 키(primary key)가 아닌 속성(Attribute)들은 기본 키에만 의존해야 한다.

**예시**

**두 번째 조건이 위반된 사례**

위 테이블에서 {Tournament, Year}가 후보키

Winner Date of Birth는 기본키가 아닌 Winner를 거쳐서 {Tournament, Year}에 의존하고 있음

⇒ 3NF 위반


따라서 테이블을 아래와 같이 둘로 나눠 줘야 함

![Untitled (86)](https://user-images.githubusercontent.com/71035113/153178337-0adb405e-eb47-46cd-a419-16cdb090e986.png)

**Q. 역정규화를 하는 이유는 무엇인가요?**

A. 정규화를 진행할 수록 하나의 테이블을 여러 테이블로 나누게 되는데, 만약 데이터 호출 시 여러 테이블을 불러서 JOIN을 해줘야한다면 이 비용도 만만치 않기 때문에 역정규화를 한다.

### 출처

- [데이터베이스 정규화 개념 설명 및 예제 – Jang (wkdtjsgur100.github.io)](https://wkdtjsgur100.github.io/database-normalization/)
