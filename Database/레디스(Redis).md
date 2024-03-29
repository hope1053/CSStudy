> Remote Dictionary Server, 메모리 기반 key-value 구조의 데이터 관리 시스템(인메모리 데이터베이스)

## Redis란?

- 모든 데이터를 메모리(RAM)에 저장하고 조회하기 때문에 빠른 Read, Write 속도를 보장하는 NoSql
    - 속도가 빠른 이유: 메모리 접근이 디스크 접근 방식보다 빠르기 때문
    - 보통 데이터베이스는 하드 디스크나 SSD에 저장
- 크게 **String, Set, Sorted Set, Hash, List** 데이터 형식 지원(다양한 자료구조 지원)

## 장점

- 리스트, 배열 데이터 처리하는데 유용
- 리스트형 데이터 입력 및 삭제가 MySQL에 비해 10배정도 빠름
- 영속적인 데이터 보존

## 백업

- Redis는 지속성 보장을 위해 데이터를 디스크에 저장할 수 있음. 서버가 내려가더라도 디스크에 저장된 데이터를 읽어서 메모리에 로딩.
- snapshot: 특정 지점을 설정하고 디스크에 백업, 순간적으로 메모리에 있는 내용을 디스크에 전체를 옮겨 담는 방식
- AOF(Append Only File) 명령을 저장해두고 서버가 셧다운되면 재실행해서 다시 만들어놓는 것