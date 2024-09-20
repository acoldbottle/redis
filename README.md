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
 

## List형
- 특징
  - 문자열 컬렉션
  - 삽입 순서를 유지
  - 스택(stack), 큐(queue) 등으로 사용하기 좋음

- 사용 예시
  - 스택
  - 큐
  - SNS 최근 게시물
  - 로그

- 명령어
  - 리스트 왼쪽부터 값을 가져오고 삭제하기[O(N)] -> LPOP key [count]
  - 리스트 왼쪽부터 값을 삽입하기[O(N)] -> LPUSH key element [element...]
  - 리스트 오른쪽부터 값을 가져오고 삭제하기[O(N)] -> RPOP key [count]
  - 리스트 오른쪽부터 값을 삽입하기[O(N)] -> RPUSH key element [element...]
  - 리스트의 왼쪽 혹은 오른쪽부터 여러 개의 값을 가져오고 삭제하기[O(N+M)] -> LMPOP numkeys key [key...]
  - 리스트에서 지정한 인덱스에 값을 조회하기[O(N)] -> LINDEX key index
  - 리스트에서 지정한 인덱스에 값을 삽입하기[O(N)] -> LINSERT key BEFORE|AFTER pivot element
  - 리스트의 길이 가져오기[O(1)] -> LLEN key
  - 리스트에서 지정한 범위의 인덱스에 있는 값 가져오기[O(S+N)] -> LRANGE key start stop
  - 리스트에서 지정한 요소를 지정한 수만큼 삭제하기[O(N+M)] -> LREM key count element
  - 리스트에서 지정한 인덱스에 있는 값을 지정한 값으로 저장하기[O(N)] -> LSET key index element


## Hash형
- 특징
  - 순서 없이 필드와 값이 여러 쌍으로 매핑된 자료구조
  - 키에 사용자별로 매핑하여 다룰 수 있음

- 사용 예시
  - 객체 표현(각 사용자를 객체로 간주하여 사용자별로 이름, 나이 등 정보를 저장하는 경우)

- 명령어
  - 해시에서 지정한 필드 삭제하기[O(N)] -> HDEL key field
  - 해시에 지정한 필드가 존재하는지 확인하기[O(1)] -> HEXISTS key field
  - 해시에 지정한 필드값 가져오기[O(1)] -> HGET key field
  - 해시에서 모든 필드 및 저장된 값 쌍 가져오기[O(N)] -> HGETALL key
  - 해시에 포함된 필드 수 가져오기[O(1)] -> HLEN key
  - 해시에서 여러 필드와 값의 쌍 저장하기[O(N)] -> HMSET key field value
  - 해시에 지정한 필드값 저장하기[O(N)] -> HSET key field value
  - 해시의 모든 필드값 가져오기[O(N)] -> HVALS key
  - 반복 처리하여 해시의 필드와 그에 연결된 값의 쌍 목록을 가져오기[O(1)] -> HSCAN key cursor [MATCH pattern] [COUNT count]
  - 해시에 지정한 필드값을 지정한 정수만큼 증가[O(1)] -> HINCRBY key field increment
  - 해시에 필드가 존재하지 않는 것을 확인한 후 값 저장하기[O(1)] -> HSETNX key field value


## Set형
-특징
  - 순서 없이 고유한 문자열 집합
  - 대상 요소 포함 여부 확인 가능
  - 집합 간 합집합, 차집합 등 작업을 통해 공통 요소 또는 차이점 추출 가능

- 사용 예시
  - 멤버십
  - 태그 관리
  - 특정 기간의 고유한 사용자 수 조사
      - HyperLogLog라는 기능은 다소 오차가 있지만 메모리를 절약하면서 고유 사용자 계산 가능

- 명령어
  -  집합에 하나 이상의 멤버 추가하기[O(1)] -> SADD key member [member ...]
  -  집합에 포함된 멤버의 수 가져오기[O(1)] -> SCARD key
  -  집합에 지정한 멤버가 포함되었는지 판단하기[O(1)] -> SISMEMBER key member
  -  집합에 포함된 모든 멤버 가져오기[O(N)] -> SMEMBERS key
  -  집합에 포함된 멤버를 무작위로 가져오기[O(1)] -> SPOP key [count]
  -  집합에서 하나 이상 멤버를 삭제하기[O(1)] -> SREM key member [member ...]
  -  반복 처리하여 멤버 목록 가져오기[O(1)] -> SSCAN key member [member ...]
  -  집합 간 차집합 가져오기[O(N)] -> SDIFF key [key ...]
  -  집합 간 차집합을 가져오고 저장하기[O(N)] -> SDIFFSTORE destination key [key]
  -  집합 간 교집합 가져오기[O(N*M)] -> SINTER key [key ...]
  -  집합 간 교집합을 가져오고 저장하기[O(N*M)] -> SINTERSTORE destination key [key ...]
  -  집합 간 교집합에 포함된 멤버 수 가져오기[O(N*M)] -> SINTERCARD numkeys key [key ...] [LIMIT limit]
  -  집합 간 합집합 가져오기[O(N)] -> SUNION key [key ...]
  -  집합에 지정한 여러 멤버가 포함되어 있는지 판단하기[O(N)] -> SMISMEMBER key member [member ...]




























    



