# REST API

### REST API

REST 아키텍처의 조건을 따르는 어플리케이션 프로그래밍 인터페이스를 뜻한다. 

**REST란?**

소프트웨어 아키텍처의 한 형식이다. 

REST 아키텍처는 여러 개의 제약 조건을 가지고 있다. 

Represntational State Transfer의 줄임말로 표현, 상태, 전달 의미

즉, 자원의 표현을 가지고 상태를 전달한다는 뜻

> 자원의 표현 ⇒ `HTTP URI`
상태 전달 ⇒ `HTTP Method`
> 

**RESTful 하다는 것?**

REST라는 아키텍처 스타일의 제약조건을 모두 만족하는 시스템

HTTP Methond와 Status code를 용도에 맞게 써야하고, 

HTTP 헤더와 Link를 신경쓰면 Restful한 서비스를 설계할 수 있다 

### **REST의 Method와 Resource**

[Click for Method](https://www.notion.so/69daf2e55ef44c539debd65e7d4ae27d)

- idempotent : 한 번 수행하냐, 여러 번 수행했을 때 결과가 같나?

### **Resource**

- http://myweb/users와 같은 URI
- 모든 것을 Resource (명사)로 표현하고, 세부 Resource에는 id를 붙임
- Message
    - 메시지 포맷이 존재
        
        : JSON, XML 과 같은 형태가 있음 (최근에는 JSON 을 씀)
        
        ```cpp
        HTTP POST, http://myweb/users/
        {
        	"users" : {
        		"name" : "terry"
        	}
        }
        ```
        

### REST 특징

- Uniform Interface
    - HTTP 표준만 맞는다면, 어떤 기술도 가능한 Interface 스타일
        
        예) REST API 정의를 HTTP + JSON로 하였다면, C, Java, Python, IOS 플랫폼 등 특정 언어나 기술에 종속 받지 않고, 모든 플랫폼에 사용이 가능한 Loosely Coupling 구조
        
- Statelessness
    - 즉, HTTP Session과 같은 컨텍스트 저장소에 **상태 정보 저장 안함**
    - *Request만 Message로 처리**하면 되고, 컨텍스트 정보를 신경쓰지 않아도 되므로, **구현이 단순해짐**.
    - 따라서, REST API 실행중 실패가 발생한 경우, Transaction 복구를 위해 기존의 상태를 저장할 필요가 있다. (POST Method 제외)
- Client-Server Architecture
- Cache Ability
