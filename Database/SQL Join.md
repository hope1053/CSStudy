# SQL JOIN

**1. Join이란?**

- 두 개 이상의 테이블을 서로 연결하여 데이터를 검색하는 방법으로

      두 개의 테이블을 **마치 하나의 테이블**인 것처럼 보여줌

- 이때, 테이블을 연결하려면 적어도 하나의 컬럼을 서로 공유하고 있어야 함

**2. 기본 구조**

```sql
SELECT 테이블.컬럼, 테이블.컬럼
FROM 테이블1, 테이블2
WHERE 조건
```

**3. Join 의 종류**

- Inner Join
- Left Outer Join
- Right Outer Join
- Full Outer Join
- Cross Join
- Self Join

<img width="500" src="https://blog.kakaocdn.net/dn/b8YNAm/btrbCuoZPrI/lEIcImHWTIZs3nApw0Bqr0/img.png">

**1) 내부 조인 (Inner Join)**

- 쉽게 말해서 교집합이라고 생각하면 됨
- 기준 테이블과 Join한 테이블의 중복된 값을 보여줌
    
    ⇒ 보통은 from 절 다음에 오는게 기준 테이블이고, 업무상 효율적인 데이터를 뽑을 수 있는 테이블을 기준 테이블로 설정한다고 함
    
- 결과값은 A테이블과 B테이블이 모두 가지고 있는 데이터만 검색됨

![Untitled (73)](https://user-images.githubusercontent.com/71035113/153177294-ed222abc-2635-4aba-9a3b-da8237f6283f.png)

```sql
1)
SELECT 테이블별칭.조회할칼럼,
테이블별칭.조회할칼럼
FROM 기준테이블 별칭
INNER JOIN 조인테이블 별칭 
ON 기준테이블별칭.기준키 = 조인테이블별칭.기준키...

2)
SELECT
A.NAME, B.AGE --B 테이블의 AGE조회
FROM EX_TABLE A -- A테이블의 별칭
INNER JOIN JOIN_TABLE B -- B테이블 별칭
ON A.NO_EMP = B.NO_EMP AND A.DEPT = B.DEPT -- 조건
```

**예시**

기준 테이블인 Sales 테이블에 

조인 테이블인 Countries 테이블의 Country를 붙이고 싶은 경우

```sql
SELECT Sales.*, Countries.Country 
FROM Sales 
JOIN Countries
ON Sales.CountryID = Countries.ID
```

<img width="500" src="https://blog.kakaocdn.net/dn/c7kLBI/btrbquYTQ0x/M4kso0nOk1n1kplQmyjHXk/img.png">

2) **Left Outer Join (=Left Join)**

- 기준 테이블의 값 + 기준 테이블과 조인 테이블의 중복된 값
- 왼쪽 테이블을 기준으로 JOIN을 하겠다
- 결과값은 A테이블의 모든 데이터와 A테이블과 B테이블의 중복되는 값이 검색됨

![Untitled (74)](https://user-images.githubusercontent.com/71035113/153177298-a4ad785f-2a8a-4a3b-80ec-b137ac5f16eb.png)

```sql
SELECT
테이블별칭.조회할칼럼,
테이블별칭.조회할칼럼
FROM 기준테이블 별칭
LEFT OUTER JOIN 조인테이블 별칭 
ON 기준테이블별칭.기준키 = 조인테이블별칭.기준키...

--예제--
SELECT
A.NAME, --A 테이블의 NAME조회
B.AGE --B테이블의 AGE조회
FROM EX_TABLE A
LEFT OUTER JOIN JOIN_TABLE B 
ON A.NO_EMP = B.NO_EMP AND A.DEPT = B.DEPT
```

- 왼쪽 테이블을 기준으로 일치하는 행만 결합되고, **일치하지 않는 부분은 null 값으로 채워짐.**
- 예시
    
    ```sql
    SELECT * 
    FROM instructor
    LEFT OUTER JOIN teaches 
    ON instructor.id = teaches.id
    ```
    
    ![https://blog.kakaocdn.net/dn/x7aO7/btrbwg59qDG/CJu4asfXeRFAX7o0fm7NdK/img.png](https://blog.kakaocdn.net/dn/x7aO7/btrbwg59qDG/CJu4asfXeRFAX7o0fm7NdK/img.png)
    

3) **Right Join (=Right Outer Join)**

![Untitled (75)](https://user-images.githubusercontent.com/71035113/153177300-2f0d521a-8ce0-4c8b-96ad-2a27d8eea8b4.png)

- 오른쪽 테이블을 기준으로 일치하는 행만 결합되고, 일치하지 않는 부분은 null 값으로 채워짐.

```sql
-- 예제
SELECT
A.NAME, B.AGE 
FROM EX_TABLE A
RIGHT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP AND A.DEPT = B.DEPT
```

- 예시
    
    ```sql
    SELECT * 
    FROM instructor
    RIGHT OUTER JOIN teaches -- 오른쪽 테이블인 teaches를 기준으로 매칭이 된다!!
    ON instructor.id = teaches.id
    ```
    
    ![https://blog.kakaocdn.net/dn/kBoPJ/btrbpWOcIGj/ECN1TsGyFcMSOOVLE1C4ok/img.png](https://blog.kakaocdn.net/dn/kBoPJ/btrbpWOcIGj/ECN1TsGyFcMSOOVLE1C4ok/img.png)
    

4) **Full Outer Join**

- 합집합을 말함
- A테이블과 B테이블의 모든 데이터가 검색됨

![Untitled (76)](https://user-images.githubusercontent.com/71035113/153177303-bb44576c-c631-4b34-833d-5c4b9f174001.png)

```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
FULL OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

**특징**

- 공통된 부분만 골라 결합하는 Inner Join 과 다르게 공통되지 않은 행도 유지한다.
- 이때 두 테이블 모두의 값을 유지하면 Full Outer Join
    - 왼쪽 테이블 값만 유지하면 Left Outer Join
    - 오른쪽 테이블 값만 유지하면 Right Outer Join
- MySQL에서는 FULL OUTER JOIN을 지원하지 않으므로 LEFT OUTER JOIN 결과와 RIGHT OUTER JOIN결과를 UNION 하여 사용해야 함
- 예시
    
    ```sql
    SELECT * FROM instructor
    FULL OUTER JOIN teaches 
    ON instructor.id = teaches.id
    ```
    
    ![https://blog.kakaocdn.net/dn/PNNRB/btrbCtcAR3w/oXmkrdq6IHzv6NggOR0kl0/img.png](https://blog.kakaocdn.net/dn/PNNRB/btrbCtcAR3w/oXmkrdq6IHzv6NggOR0kl0/img.png)
    

![Untitled (77)](https://user-images.githubusercontent.com/71035113/153177304-79b7d802-7953-4002-a1e0-788d6fc52e41.png)

5) **Cross Join (곱집합)**

![Untitled (78)](https://user-images.githubusercontent.com/71035113/153177307-113cb845-85be-47ed-a492-f6aa5473e308.png)

- 모든 경우의 수를 전부 표현해주는 방식으로 두 테이블 데이터의 모든 조합을 볼 수 있음
- (테이블1의 row) * (테이블2의 row) 개수만큼의 row를 가진 테이블 생성 ⇒ 여기서는 총 12개

```sql
1)
SELECT 조회할컬럼들
FROM 테이블1, 테이블2 -- 기준테이블과 조인테이블

2)
SELECT 조회할컬럼들
FROM 테이블1
CROSS JOIN 테이블2
```

![https://blog.kakaocdn.net/dn/lBWZk/btrbHcvQ7lK/ziZIwcRD2XedQRGznmbmUk/img.png](https://blog.kakaocdn.net/dn/lBWZk/btrbHcvQ7lK/ziZIwcRD2XedQRGznmbmUk/img.png)

**6) Self Join**

![Untitled (79)](https://user-images.githubusercontent.com/71035113/153177310-4807e33e-9626-4d62-85d3-4cc1ada0b3ca.png)

- 자기자신과 자기자신을 조인하는 것이다.
- 하나의 테이블을 여러번 복사해서 조인한다고 생각하면 편하다.
- 자신이 갖고 있는 칼럼을 다양하게 변형시켜 활용할 때 자주 사용한다.
