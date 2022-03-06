# **TLS/SSL HandShake**

`HTTPS에서 클라이언트와 서버간 통신 전 SSL 인증서로 신뢰성 여부를 판단하기 위해 연결하는 방식`

### SSL **인증서로 서버가 신뢰할 수 있는지 어떻게 판단할까?**

위에서 말했던 `공개키 서명`방식을 사용한다. 브라우저는 신뢰할 수 있는 사이트와 그 사이트의 공개키를 미리 가지고 있다. 웹 브라우저가 서버에 접속한다면

1. 서버는 CA가 발급한 SSL 인증서를 제공한다. 이 인증서에는 서버측의 공개키와 서비스의 정보를 담고있다.
2. 브라우저는 이 인증서를 발급한 CA(certificate authority)가 자신의 CA 리스트에 있는지 확인한다.
    1. SSL인증서를 기준으로 클라이언트가 접속한 서버가 클라이언트가 의도한 서버가 맞는지를 확인을 하게 된다. 이러한 일을 해주는 공인된 회사들을 CA라고 한다. 이러한 CA는 브라우저가 리스트를 가지고 있고 이 CA들의 `공개키`들을 가지고 있다
3. CA가 리스트에 있다면 CA의 해당 공개키를 이용해서 인증서를 복호화한다. **복호화가 된다면 이 인증서는 CA의 비공개키에 의해 암호화 되었다는 것을 알 수 있다.**

### **진행 순서 (CA인증 확인 ⇒ 공개키 ⇒ 대칭키)**

1. 클라이언트는 서버에게 `client hello` 메시지를 담아 서버로 보낸다. 이때 암호화된 정보를 함께 담는데, `버전`, `암호 알고리즘`, `압축 방식` 등을 담는다.
    
    ![https://user-images.githubusercontent.com/34904741/139517776-f2cac636-5ce5-4815-981d-33905283bf13.png](https://user-images.githubusercontent.com/34904741/139517776-f2cac636-5ce5-4815-981d-33905283bf13.png)
    
2. 서버는 클라이언트가 보낸 암호 알고리즘과 압축 방식을 받고, `세션 ID`와 `CA 공개 인증서`를 `server hello` 메시지와 함께 담아 응답한다. 이 CA 인증서에는 앞으로 통신 이후 사용할 대칭키가 생성되기 전, 클라이언트에서 handshake 과정 속 암호화에 사용할 공개키를 담고 있다.
3. 클라이언트 측은 서버에서 보낸 CA 인증서에 대해 유효한 지 CA 목록에서 확인하는 과정을 진행한다.
4. CA 인증서에 대한 신뢰성이 확보되었다면, 클라이언트는 난수 바이트를 생성하여 서버의 공개키로 암호화한다.
    
    ![https://user-images.githubusercontent.com/34904741/139517776-f2cac636-5ce5-4815-981d-33905283bf13.png](https://user-images.githubusercontent.com/34904741/139517776-f2cac636-5ce5-4815-981d-33905283bf13.png)
    
5. 만약 2번 단계에서 서버가 클라이언트 인증서를 함께 요구했다면, 클라이언트의 인증서와 클라이언트의 개인키로 암호화된 임의의 바이트 문자열을 함께 보내준다.
6. 서버는 클라이언트의 인증서를 확인 후, 난수 바이트를 자신의 개인키로 복호화 후 대칭 마스터 키 생성에 활용한다.
7. 클라이언트는 handshake 과정이 완료되었다는 `finished` 메시지를 서버에 보내면서, 지금까지 보낸 교환 내역들을 해싱 후 그 값을 대칭키로 암호화하여 같이 담아 보내준다.
8. 서버도 동일하게 교환 내용들을 해싱한 뒤 클라이언트에서 보내준 값과 일치하는 지 확인한다. 일치하면 서버도 마찬가지로 `finished` 메시지를 이번에 만든 대칭키로 암호화하여 보낸다.
9. 클라이언트는 해당 메시지를 대칭키로 복호화하여 서로 통신이 가능한 신뢰받은 사용자란 걸 인지하고, 앞으로 클라이언트와 서버는 해당 대칭키로 데이터를 주고받을 수 있게 된다.

### **참고 자료**

- [링크](https://wangin9.tistory.com/entry/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EC%97%90-URL-%EC%9E%85%EB%A0%A5-%ED%9B%84-%EC%9D%BC%EC%96%B4%EB%82%98%EB%8A%94-%EC%9D%BC%EB%93%A4-5TLSSSL-Handshake)