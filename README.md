# redis
참고 서적 : 실전 레디스 (하야시 쇼고)

## 레디스(redis)란 ?
- 비관계형 데이터베이스(NoSQL)
- 인메모리 데이터 구조 저장소로써 인메모리에서 빠르게 동작
- [자료형](#자료형)과 기능 및 관련 명령어가 다양
- 데이터 영속성 기능
- 레플리케이션/클러스터 기능을 통한 확장성 및 가용성이 높음
- 클라이언트/서버 모델 기반의 요청/응답 통신
- 싱글 스레드 요청 이벤트를 주도적으로 처리


# 자료형
1. [String형](#string형)
2. [List형](#list형)
3. [Hash형](#hash형)
4. [Set형](#set형)
5. [Sorted-Set형](#sorted-set형)



## String형
- 특징
  - 키에 값을 일대일로 대응시키는 가장 간단한 자료형
  - 이진 안전 문자열

- 사용 예시
  - 캐시
    - 간단한 키와 값의 쌍으로 대응되는 문자열
    - 세션 정보
    - 이미지 데이터 등 이진 데이터
  - 카운터
    - 방문자 수 등 접근 수 카운트
  - 실시간 매트릭스
    - 각 항목의 수치를 파악할 수 있는 지표 등
   
- 명령어
  - 키값 가져오기[O(1)] -> GET key
  - 키에 값 저장하기[O(1)] -> SET key value
  - 여러개의 키값 가져오기[O(N)] -> MGET key
  - 여러개의 키에 값을 저장하기[O(N)] -> MSET key value
  - 키에 값 덮어쓰기[O(1)] -> APPEND key value
  - 키의 길이 가져오기[O(1)] -> STRLEN key
  - 범위를 지정하여 키값 가져오기[O(N)] -> GETRANGE key start end
  - 범위를 지정하여 키값 저장하기[O(1)] -> SETRANGE key offset value
  - 값을 1만큼 증가시키기[O(1)] -> INCR key
  - 값을 지정한 정수만큼 증가시키기[O(1]) -> INCRBY key increment
  - 값을 지정한 부동소수점만큼 증가시키기[O(1)] -> INCRBYFLOAT key increment
  - 값을 1만큼 감소시키기[O(1)] -> DECR key
  - 값을 지정한 정수만큼 감소시키기[O(1)] -> DECRBY key decrement
  - TTL을 설정한 키값 가져오기[O(1)] -> GETEX key
  - 키 값을 가져온 후 그 키를 삭제하기[O(1)] -> GETDEL key
  - 여러 개의 키가 존재하지 않는 것을 확인하고 값을 저장하기[O(N)] -> MSETNX key value
    



