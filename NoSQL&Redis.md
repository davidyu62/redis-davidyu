# Chapter 01. Redis란

redis는 NoSQL중 Key,Value구조로 데이터를 저장하는 대표 제품이다.

- Redis DB는 인메모리 기반의 데이터 저장 구조이다.
  - 1차적으로 모든 데이터는 메모리에 저장되며, 사용자 명령어 또는 시스템 환경 설정 방법들을 통해 필요에 따라 선택적으로 디스크에 저장한다.
- Key Value 데이터 구조는 하나의 Key와 데이터 값으로 구성된다.
  - 데이터 저장 구조를 테이블이라고 표현한다. 인덱스를 생성할 수 있지만 인덱스의 종류 및 구조는 많이 다르기 때문에 표현에는 한계가 있다.
- 가공처리가 요구되는 비즈니스 환경에서 적합하다.
  - 보통 데이터의 가공처리, 통계 분석, 데이터 캐싱, 메시지 큐 등의 용도로 사용된다.

# Chaptor 02. Redis 설치 및 데이터 처리

## 주요 특징

- Redis는 키밸류 데이터베이스로 분류되는 NoSQL이다.
- In Memory 기반의 데이터 처리 및 저장기술을 제공하기 때문에 다른 NoSQL 제품에 비해 상대적으로 빠른 Read/Write가 가능하다.
- String, Set, Sorted Set, Hash, List, HyperLogLogs 유형의 데이터를 저장할 수 있다.
- Dump 파일과 AOF 방식으로메모리 상의 데이터를 디스크에 저장할 수 있다.
- Master/Slave Replication 기능을 통해 데이터의 분산, 복제 기능을 제공하며 Query Off Loading 기능을 통해 Master는 Read/Write를 수행하고, Slave는 Read만 수행할 수 있다.
- 파티셔닝을 통해 동적인 스케일 아웃인 수평 확장이 가능하다
- Expiration 기능은 일정 시간이 지났을 때 메모리 상의 데이터를 자동 삭제할 수 있다.

## Redis 설치 및 실행

- https://redis.io/download/ 에서 설치파일 다운로드
- 압축을 푼 후 해당 디렉토리로 들어가서 빌드를 한다.

```sh
[lena@LNJDUWS2 redis-7.0.9]$ yum -y install gcc-c++
[lena@LNJDUWS2 redis-7.0.9]$ make distclean
[lena@LNJDUWS2 redis-7.0.9]$ make
```

Redis Server 시작

````sh
[lena@LNJDUWS2 src]$ ./redis-server ../redis.conf
165578:C 18 Jul 2023 16:17:21.642 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
165578:C 18 Jul 2023 16:17:21.642 # Redis version=7.0.9, bits=64, commit=00000000, modified=0, pid=165578, just started
165578:C 18 Jul 2023 16:17:21.642 # Configuration loaded
165578:M 18 Jul 2023 16:17:21.643 * Increased maximum number of open files to 10032 (it was originally set to 8192).
165578:M 18 Jul 2023 16:17:21.643 * monotonic clock: POSIX clock_gettime
                _._
           _.-``__ ''-._
      _.-``    `.  `_.  ''-._           Redis 7.0.9 (00000000/0) 64 bit
  .-`` .-```.  ```\/    _.,_ ''-._
 (    '      ,       .-`  | `,    )     Running in standalone mode
 |`-._`-...-` __...-.``-._|'` _.-'|     Port: 5000
 |    `-._   `._    /     _.-'    |     PID: 165578
  `-._    `-._  `-./  _.-'    _.-'
 |`-._`-._    `-.__.-'    _.-'_.-'|
 |    `-._`-._        _.-'_.-'    |           https://redis.io
  `-._    `-._`-.__.-'_.-'    _.-'
 |`-._`-._    `-.__.-'    _.-'_.-'|
 |    `-._`-._        _.-'_.-'    |
  `-._    `-._`-.__.-'_.-'    _.-'
      `-._    `-.__.-'    _.-'
          `-._        _.-'
              `-.__.-'

165578:M 18 Jul 2023 16:17:21.644 # WARNING: The TCP backlog setting of 511 cannot be enforced because /proc/sys/net/core/somaxconn is set to the lower value of 128.
165578:M 18 Jul 2023 16:17:21.644 # Server initialized
165578:M 18 Jul 2023 16:17:21.645 * Ready to accept connections
````

Redis Client 시작

```sh
[lena@LNJDUWS2 src]$ ./redis-cli -p 5000
127.0.0.1:5000>
```

## Data 처리

### 용어 설명

- Table : 하나의 DB에서 데이터를 저장하는 노리적 구조(과계형 DB에서 말하는 Table과 동일하다)
- Data Sets : 테이블을 구성하는 논리적 단위. 하나의 데이터 셋은 하나의 Key와 하나 이상의 Field/Element로 구성된다.
- Key : 하나의 Key는 하나 이상의 조합된 값으로 표현 가능하다
- Values : 해당 Key에 대한 구체적인 데이터 값을 표현한다.

### 데이터 타입

- strings : 문자, Binary 유형 데이터를 저장
- List : 하나의 Key에[ 여러 개의 배열 값을 저장]
- Hash : 하나의Key에 여러 개의 Fields와 Value로 구성
- Set Sorted set : 정렬되지 않은 String 타입
- Sorted Set : Set과 Hash를 결합한 타입
- Bitmaps : 0 & 1 로 표현하는 데이터 타입
- HyperLogLogs : Element 중에서 Unique 한 개수의 Element만 계산
- Geospatial : 좌표 데이터를 저장 및 관리하는 데이터 타입

# Chapter 03. 트랜잭션 제어 & 사용자 관리

## 트랜잭션 제어

- 추후에 작성 예정

## 사용자 관리

### 엑세스 컨트롤 권한

- 미리 DB내에 사용자 계정과 암호를 생성해 두고 Redis 서버에 접속하려는 사용자는 해당 계정과 암호를 입력하여 허가 받는 방법

### 인증 방법

1. 운영체제 인증방법
   conf파일에 접속할 클라이언트의 ip-address를 미리 지정하는 방법
2. Internal 인증 방법
   Redis 서버에 접속한 다음 auth 명령어로 미리 생성해둔 사용자 계정과 암호를 입력하여 권한을 부여 받는 방법

# Chapter 04. Redis Data Modeling

추후 작성

# Chapter 05. Redis Architecture

## 아키텍처

![img](.//images//redis_architecture.PNG)

### 메모리 영역

- Resident Area : 이 영역은 사용자가 Redis 서버에 접속해서 처리하는 모든 데이터가 가장 먼저 저장되는 영역이며, 실제 작업이 수행되는 공간이고 WorkingSet 영역이라고도 표현한다.
- Data Structure : Redis 서버를 운영하다 보면 발생하는 다양한 정보와 서버 상태를 모니터링 하기 위해 수집한 상태 정보를 저장하고 관리하기 위한 메모리 공간이 필요하다. 이를 저장하는 메모리 영역을 Data Structure 영역이라고 한다.

### 파일 영역

- AOF 파일 : Redis는 In-Memory 기반의 데이터 처리기술을 활용하나, 중요한 데이터의 경우 사용자의 필요에 따라 저장할 필요가 있는데 이 디스크 영역이 AOF 파일이다.
- DUMP 파일 : AOF파일과 비슷한 용도나, 소량의 데이터를 일지적으로 저장할 때 사용되는 파일이다.

### 프로세스 영역

- Server Process : redis-server.sh, redis-sentinel.sh 실행 코드에 의해 활성화되는 프로세스
- Client Process : redis-cli.sh에 의해 실행되는 프로세스

## 시스템 & Disk 사양

### 노드 수

하나의 Standalone 서버를 구축하는 경우에 Master 서버 1대, Slave 서버 1대, Failover & Load-Balancing을 위한 Sentinel 서버1대로 구성하는 경우 최소 3대의 서버가 요구된다. Sentinel 서버는 최소 사양으로 구축 한다.

### CPU Core 수

- Small Business 환경 : 4 Core 이하
- Medium Business 환경 : 4 ~ 8 Core 이하
- Big Business 환경 : 8 ~ 16 Core 이상

### RAM

_추후 작성_

### 스토리지

_추후 작성_

### 네트워크

_추후 작성_

## 메모리 운영 기법

### LRU 알고리즘

가장 최근에 처리된 데이터들을 메모리 영역에 최대한 재 배치시키는 알고리즘이다. 최근에 처리된 데이터일 경우 오래된 데이터보다 사용될 확률이 1%라도 높기 때문이다.

```sh
$ vi redis.conf
Maxmemory   3000000000      # Redis 인스턴스를 위한 총 메모리 크기
maxmemory-sample    5       # LRU 알고리즘에 의한 메모리 운영시 사용
```

### LFU 알고리즘

LRU의 단점은 모든 데이터들이 재사용 및 재 검색되는 것은 아니라는 점이다.
이를 해결하기 위해 나온 알고리즘이며, 자주 참조되는 데이터만 배치하고 그렇지 않은 데이터들은 메모리로부터 제거하는 방식이다.

```sh
$ vi redis.conf

lfu-log-factor  10  # LFU 알고리즘에 의한 메모리 운영(default:10)
lfu-decay-time  1
```

## LazyFree

인-메모리 기반의 데이터 저장 구조인 Redis는 초당 수만~수십 만 건의 데이터가 저장되는 빅데이터 환경에서 빠른 시간내에
메모리 영역이 임계치에 도달하게 된다. 이 경우, 연속적인 범위 Key 값이 동시에 삭제되는 Operation이 실행되면 메모리 부족과
프로세스의 지연처리로 인해 성능 지연문제가 발생하게 된다.
이를 해결하기 위한 방법은 LazyFree 파라메터를 설정해 주는 것이다. 이 파라메터는 별도의 백그라운드 쓰레드를 통해
입력과 삭제 작업이 지연되지 않고 연속적으로 수행될 수 있도록 한다. LazyFree 쓰레드는 Redis Architecture에서 언급한
서버 프로세스의 4개 쓰레드 중 하나이다.

```sh
$ vi redis.conf

lazyfree-lazy-eviction       no  # yes 권장(unlink로 삭제하고 새 키 저장)
lazyfree-lazy-expire         no  # yes 권장(unlink로 만기 된 키 삭제)
lazyfree-lazy-server-del     no  # yes 권장(unlink로 데이터 변경)
slave-lazy-flush             no  # yes 권장(복제 서버가 삭제 후 복제할 떄 FlushAll async 명령어로 삭제)
```

## Data Persistence

설정

```sh
$ vi redis.conf
save        60      1000    # 60초마다 1,000 Key 저장(RDB설정)

appendonly      yes                             # AOF 환경 설정
appendonlyname  "appendonly.aof"                # AOF 파일명
```

### RDB

사용자가 저장 주기와 저장 단위를 결정할 수 있고, 시스템 자원이 최소한으로 요구된다는 장점이 있다.
하지만 데이터를 최종 저장한 이후 새로운 저장이 수행되는 시점 전에 시스템 장애 발생 시 데이터의 유실이 발생 할 수 있다.

### AOF

이 방법은 redis-shell 상에서 bgrewriteaof 명령어를 실행한 이후에 입력,수정,삭제되는 모든 데이터를 저장해 준다.

| Append Only File                                            | RDB(SnapShot)                         |
| ----------------------------------------------------------- | ------------------------------------- |
| 시스템 자원이 집중적으로 요구                               | 시스템 자원이 최소한으로 요구         |
| 마지막 시점까지 데이터 복구가 가능                          | 지속성이 떨어짐                       |
| 대용량 데이터 파일로 복구 작업시 복수 성능이 떨어짐         | 복구 시간이 빠름                      |
| 저장 공간이 압축되지 않기 때문에 데이터 양에 따라 크기 결정 | 저장 공간이 압축되지 떄문에 최소 필요 |

## Copy on Write

_추후 작성_

# Redis Cluster 시스템 & 로그 모니터링

## 개요

데이터를 하나의 서버에 저장하지 않고 분산하여 저장을 하는데 이는 자원 공유, 성능 향상, 안정성을 확보하기 위한 방안이다.
Redis는 마스터, 슬레이브, 센티널, 파티션 클러스트 등의 기능을 통해 데이터를 복제하고 분산 처리를 합니다.

> 범위 파티션

Key값을 기준으로 데이터를 분산하여 저장한다. 예를 들어 key가 1~100은 1번 서버에 101~200은 2번 서버에 201~300은 3번 서버에
저장하는 방식이다.

> 해시 파티션

범위 파티션은 사용자가 직접 설계를 하게 되며 이 경우 데이터 양과 분산 정보가 현저히 떨어지는 경우가 발생할 수 있다.
해시 파티션은 이를 해결하기 위해 Hash Algorithm에 의해 데이터를 골고루 분산 저장할 수 있도록 해준다.

## Replication

> 개념

Redis에서 replication이란 데이터 유실을 최소화하기 위한 복사본을 만드는 이중화를 뜻한다.
아래는 Replication 한 예시이다.

![img](.//images//replication_ex1.PNG)

master server가 존재하고 두개의 slave서버가 master 서버를 바라보는 architecuture이다.  
master server의 데이터가 실시간으로 slave 서버로 복제가 되며, slave 서버는 master 서버에 의해 쓰기 작업만 수행가능하며 사용자는 오로지 읽기 작업만 수행 가능하다. 위처럼 구성을 하더라도 <b>master server가 장애가 발생할 경우 자동으로 slave서버로 failover가 되지는 않는다.</b> 다만 slave server에 복제된 데이터를 이용하여 master server를 복구할 수는 있다.

이것은 우리가 알고 있는 진정한 의미의 HA 구성은 아니다.이를 해결하기 위해서는 Sentinel 서버가 필요하다.  
_<h3>What is Sentinel</h3>_

sentinel은 failover를 지원하는 서버라고 이해하면 된다. master를 모니터링하다가 master가 죽었다고 판단될 시 slave를 master로 승격시킴으로써 reids의 availibility를 보장한다.  
![img](.//images//replication_ex2.PNG)

> 실습

실습예제1) master서버 1대와 slave 서버 2대 연동

_<h3>Step1</h3>_
redis-master-5001.conf 파일 작성

```conf
bind 127.0.0.1        # 해당 IP로 접속하는 Client만 받아들이는 기능
port 6379
daemonize  yes        # daemon으로 실행
```

redis-slave-5003.conf, 5004 파일 작성

```conf
bind 127.0.0.1
port 5003(slave -1) / port 5004(slave-2)
replicaof 127.0.0.1 5001                  # master server ip, port
daemonize yes
```

_<h3>Step2</h3>_
서버 기동

```sh
[lena@LNJDUWS2 redis-replication]$ ./src/redis-server redis-master-5001.conf
[lena@LNJDUWS2 redis-replication]$ ./src/redis-server redis-slave-5003.conf
[lena@LNJDUWS2 redis-replication]$ ./src/redis-server redis-slave-5004.conf
[lena@LNJDUWS2 redis-replication]$ ps -ef | grep redis
lena     3175558       1  0 09:58 ?        00:00:00 ./src/redis-server 127.0.0.1:5001
lena     3175606       1  0 09:58 ?        00:00:00 ./src/redis-server 127.0.0.1:5003
lena     3175638       1  0 09:58 ?        00:00:00 ./src/redis-server 127.0.0.1:5004
lena     3175668 3164384  0 09:58 pts/0    00:00:00 grep --color=auto redis

```

※ replication 을 사용하기 위해서는 conf 파일에 cluster-enabled 값이 no로 setting되어야 한다.  
 default값은 yes이므로 no로 변경이 필요하다. yes일 경우 기동 오류 발생함

_<h3>Step3</h3>_

replication 확인

```sh
[lena@LNJDUWS2 redis-replication]$ ./src/redis-cli -p 5001      # master 서버 접속
127.0.0.1:5001> set lg cns
OK
127.0.0.1:5001> exit
[lena@LNJDUWS2 redis-replication]$ ./src/redis-cli -p 5003      # slave 1 접속
127.0.0.1:5003> get lg
"cns"
127.0.0.1:5003> exit
[lena@LNJDUWS2 redis-replication]$ ./src/redis-cli -p 5004      # slave 2 접속
127.0.0.1:5004> get lg
"cns"
```

실습예제2) master, slave, sentinel 연동
_<h3>Step1</h3>_
sentinel.conf 수정(총 3개의 conf 파일을 만든다)

```conf
# sentinel monitor <master-name> <ip> <redis-port> <quorum>
sentinel monitor lat-master 127.0.0.1 5001 2
```

_<h3>Step2</h3>_
각각의 sentinel 서버를 ./redis-server sentinel.conf 명령어를 통해 수행한다.

_<h3>Step3</h3>_
테스트

```sh
## 1대의 master, 2대의 slave, 3대의 sentinel 프로세스 확인
[lena@LNJDUWS2 redis-replication]$ ps -ef | grep redis
lena     3179326       1  0 10:08 ?        00:00:02 ./src/redis-server 127.0.0.1:5003
lena     3179346       1  0 10:08 ?        00:00:02 ./src/redis-server 127.0.0.1:5004
lena     3182765       1  0 10:17 ?        00:00:01 ./src/redis-sentinel *:26379 [sentinel]
lena     3182789       1  0 10:17 ?        00:00:03 ./src/redis-sentinel *:26389 [sentinel]
lena     3182807       1  0 10:17 ?        00:00:03 ./src/redis-sentinel *:26399 [sentinel]
lena     3185165       1  0 10:24 ?        00:00:00 ./src/redis-server 127.0.0.1:5001

# sentinel 서버 접속 후 info 확인
[lena@LNJDUWS2 redis-replication]$ ./src/redis-cli -p 26379
127.0.0.1:26379> info sentinel
# Sentinel
sentinel_masters:1
sentinel_tilt:0
sentinel_tilt_since_seconds:-1
sentinel_running_scripts:0
sentinel_scripts_queue_length:0
sentinel_simulate_failure_flags:0
master0:name=lat-master,status=sdown,address=127.0.0.1:5001,slaves=2,sentinels=3

# master 서버 process kill 후 5003 slave 서버 접속
[lena@LNJDUWS2 redis-replication]$ kill -9 3185165
[lena@LNJDUWS2 redis-replication]$ ps -ef | grep redis
lena     3179326       1  0 10:08 ?        00:00:02 ./src/redis-server 127.0.0.1:5003
lena     3179346       1  0 10:08 ?        00:00:02 ./src/redis-server 127.0.0.1:5004
lena     3182765       1  0 10:17 ?        00:00:01 ./src/redis-sentinel *:26379 [sentinel]
lena     3182789       1  0 10:17 ?        00:00:03 ./src/redis-sentinel *:26389 [sentinel]
lena     3182807       1  0 10:17 ?        00:00:03 ./src/redis-sentinel *:26399 [sentinel]
127.0.0.1:5003> info replication
# Replication
role:slave
master_host:127.0.0.1
master_port:5004                    ## master 서버가 5004 slave 서버로 변경됨을 볼 수 있다.
master_link_status:up
master_last_io_seconds_ago:0
master_sync_in_progress:0
slave_read_repl_offset:273053
slave_repl_offset:273053
slave_priority:100
slave_read_only:1
replica_announced:1
connected_slaves:0
master_failover_state:no-failover
master_replid:feecd652b657966d06f336483116fa1b0c364449
master_replid2:1817233988556458e0d1548291e489c7c81d74a9
master_repl_offset:273053
second_repl_offset:10242
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1118
repl_backlog_histlen:271936

# 5004 slave 서버 접속
[lena@LNJDUWS2 redis-replication]$ ./src/redis-cli -p 5004
127.0.0.1:5004> info replication
# Replication
role:master                           ## role이 master임을 알 수 있다.
connected_slaves:1
slave0:ip=127.0.0.1,port=5003,state=online,offset=283653,lag=0
master_failover_state:no-failover
master_replid:feecd652b657966d06f336483116fa1b0c364449
master_replid2:1817233988556458e0d1548291e489c7c81d74a9
master_repl_offset:283923
second_repl_offset:10242
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1118
repl_backlog_histlen:282806

# master 서버(5001) 기동 후 5004 slave 서버의 role 확인
[lena@LNJDUWS2 redis-replication]$ ./src/redis-server ./redis-master-5001.conf
[lena@LNJDUWS2 redis-replication]$ ps -ef | grep redis
lena     3179326       1  0 10:08 ?        00:00:05 ./src/redis-server 127.0.0.1:5003
lena     3179346       1  0 10:08 ?        00:00:04 ./src/redis-server 127.0.0.1:5004
lena     3182765       1  0 10:17 ?        00:00:04 ./src/redis-sentinel *:26379 [sentinel]
lena     3182789       1  0 10:17 ?        00:00:08 ./src/redis-sentinel *:26389 [sentinel]
lena     3182807       1  0 10:17 ?        00:00:08 ./src/redis-sentinel *:26399 [sentinel]
lena     3194103       1  0 10:48 ?        00:00:00 ./src/redis-server 127.0.0.1:5001

[lena@LNJDUWS2 redis-replication]$ ./src/redis-cli -p 5004
127.0.0.1:5004> info replication
# Replication
role:master                                             ## failback이 이루어지지 않음(추후 확인 필요)
connected_slaves:2
slave0:ip=127.0.0.1,port=5003,state=online,offset=327184,lag=0
slave1:ip=127.0.0.1,port=5001,state=online,offset=327184,lag=0
master_failover_state:no-failover
master_replid:feecd652b657966d06f336483116fa1b0c364449
master_replid2:1817233988556458e0d1548291e489c7c81d74a9
master_repl_offset:327319
second_repl_offset:10242
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1118
repl_backlog_histlen:326202

```

※ 외부에서 Sentinel에 접속하기 위해서는 master,slave 들이 protected-mode 가 아니거나 비밀번호를 설정해야 한다

## Clustering

> 개념

하나의 standalone 서버 만으로 처리할 수 없을 만큼 빅데이터가 발생하는 비즈니스 환경에서는 성능지연, 다양한 장애 현상이 발생하게 된다.
이를 해결하기 위한 방법으로 Redis Cluster(Shard-Replication) 이다.

![img](.//images//redis-clustering.PNG)

> 실습

클러스터링을 수동으로 설정하는 방법이며 이 외에도 redis-trib.rb 유틸리티를 이용하여 자동 설정 방법이 존재한다.
여기서는 다루지 않겠다.

```sh
[lena@LNJDUWS2 redis-cluster]$ ./src/redis-cli -p 5001 cluster meet 127.0.0.1 5003
OK
[lena@LNJDUWS2 redis-cluster]$ ./src/redis-cli -p 5001 cluster meet 127.0.0.1 5004
OK
[lena@LNJDUWS2 redis-cluster]$ ./src/redis-cli -p 5001 cluster meet 127.0.0.1 5005
OK
[lena@LNJDUWS2 redis-cluster]$ ./src/redis-cli -p 5001 cluster meet 127.0.0.1 5006
OK
[lena@LNJDUWS2 redis-cluster]$ ./src/redis-cli -p 5001 cluster meet 127.0.0.1 5002

# cluster node 확인
[lena@LNJDUWS2 redis-cluster]$ ./src/redis-cli -p 5001 cluster nodes
2b29a88d97d77ff9e0f234f218e75a8d87366dae 127.0.0.1:5003@15003 master - 0 1691041612581 3 connected 10923-16383
27993bbbab750950e9fd514c59126290bef83865 127.0.0.1:5004@15004 master - 0 1691041612000 4 connected
80eff62f0b65e7759662d59542cc043d598c1c1e 127.0.0.1:5001@15001 myself,master - 0 1691041611000 1 connected 0-5460
428f78b2035e9983be5408b55dd8496c8620f3ad 127.0.0.1:5006@15006 master - 0 1691041613184 5 connected
c38668d16da33f5f175e1e9b13f33ef8ba39f5ed 127.0.0.1:5005@15005 master - 0 1691041612581 0 connected
de288c03ffefe65905184ecc45a9defea9f0df83 127.0.0.1:5002@15002 master - 0 1691041612180 2 connected 5461-10922

# slave 서버를 각 master 서버로의 복제서버로 지정
[lena@LNJDUWS2 redis-cluster]$ ./src/redis-cli -p 5004 cluster replicate 80eff62f0b65e7759662d59542cc043d598c1c1e
OK
[lena@LNJDUWS2 redis-cluster]$ ./src/redis-cli -p 5005 cluster replicate de288c03ffefe65905184ecc45a9defea9f0df83
OK
[lena@LNJDUWS2 redis-cluster]$ ./src/redis-cli -p 5006 cluster replicate 2b29a88d97d77ff9e0f234f218e75a8d87366dae
OK

# cluster node 확인
[lena@LNJDUWS2 redis-cluster]$ ./src/redis-cli -p 5004 cluster slots
1) 1) (integer) 0         # start slot
   2) (integer) 5460      # end slot
   3) 1) "127.0.0.1"
      2) (integer) 5001               # master
      3) "80eff62f0b65e7759662d59542cc043d598c1c1e"
      4) (empty array)
   4) 1) "127.0.0.1"
      2) (integer) 5004
      3) "27993bbbab750950e9fd514c59126290bef83865"
      4) (empty array)
2) 1) (integer) 5461
   2) (integer) 10922
   3) 1) "127.0.0.1"
      2) (integer) 5002
      3) "de288c03ffefe65905184ecc45a9defea9f0df83"
      4) (empty array)
   4) 1) "127.0.0.1"
      2) (integer) 5005
      3) "c38668d16da33f5f175e1e9b13f33ef8ba39f5ed"
      4) (empty array)
3) 1) (integer) 10923
   2) (integer) 16383
   3) 1) "127.0.0.1"
      2) (integer) 5003
      3) "2b29a88d97d77ff9e0f234f218e75a8d87366dae"
      4) (empty array)
   4) 1) "127.0.0.1"
      2) (integer) 5006
      3) "428f78b2035e9983be5408b55dd8496c8620f3ad"
      4) (empty array)
```

5001번 Master 서버의 내용이 5004 Slave 서버로 복제가 잘 되었는지 확인

```sh
[lena@LNJDUWS2 redis-cluster]$ ./src/redis-cli -p 5001
127.0.0.1:5001> clear
127.0.0.1:5001> keys *
(empty array)
127.0.0.1:5001> set lg cns
OK
127.0.0.1:5001> get lg
"cns"
127.0.0.1:5001> exit
[lena@LNJDUWS2 redis-cluster]$ ./src/redis-cli -p 5004
127.0.0.1:5004> get lg
(error) MOVED 4614 127.0.0.1:5001
127.0.0.1:5004> keys *
1) "lg"
127.0.0.1:5004> get lg
(error) MOVED 4614 127.0.0.1:5001
127.0.0.1:5004> readonly                # readonly를 수행해줘야 위와 같은 error가 발생하지 않는다
OK
127.0.0.1:5004> get lg
"cns"

```

### 만약 master 서버가 다운됐을 경우?

master서버가 다운됐을 경우에는 slave 서버가 master 서버로 전환된다.

```sh
127.0.0.1:5001> auth 1234
OK
127.0.0.1:5001> cluster nodes
27993bbbab750950e9fd514c59126290bef83865 127.0.0.1:5004@15004 master,fail - 1693205776513 1693205773995 6 disconnected 0-5460
2b29a88d97d77ff9e0f234f218e75a8d87366dae 127.0.0.1:5003@15003 master - 0 1693206139544 3 connected 10923-16383
80eff62f0b65e7759662d59542cc043d598c1c1e 127.0.0.1:5001@15001 myself,slave 27993bbbab750950e9fd514c59126290bef83865 0 1693206138000 6 connected
de288c03ffefe65905184ecc45a9defea9f0df83 127.0.0.1:5002@15002 master - 0 1693206140551 2 connected 5461-10922
428f78b2035e9983be5408b55dd8496c8620f3ad 127.0.0.1:5006@15006 slave 2b29a88d97d77ff9e0f234f218e75a8d87366dae 0 1693206139000 3 connected
c38668d16da33f5f175e1e9b13f33ef8ba39f5ed 127.0.0.1:5005@15005 slave de288c03ffefe65905184ecc45a9defea9f0df83 0 1693206140000 2 connected
127.0.0.1:5001> cluster failover takeover
OK
127.0.0.1:5001> cluster nodes
27993bbbab750950e9fd514c59126290bef83865 127.0.0.1:5004@15004 master,fail - 1693205776513 1693205773995 6 disconnected
2b29a88d97d77ff9e0f234f218e75a8d87366dae 127.0.0.1:5003@15003 master - 0 1693206188159 3 connected 10923-16383
80eff62f0b65e7759662d59542cc043d598c1c1e 127.0.0.1:5001@15001 myself,master - 0 1693206188000 7 connected 0-5460
de288c03ffefe65905184ecc45a9defea9f0df83 127.0.0.1:5002@15002 master - 0 1693206189000 2 connected 5461-10922
428f78b2035e9983be5408b55dd8496c8620f3ad 127.0.0.1:5006@15006 slave 2b29a88d97d77ff9e0f234f218e75a8d87366dae 0 1693206189165 3 connected
c38668d16da33f5f175e1e9b13f33ef8ba39f5ed 127.0.0.1:5005@15005 slave de288c03ffefe65905184ecc45a9defea9f0df83 0 1693206187153 2 connected

```

## Logging & Monitoring

> Logging 정보

loglevel 파라미터를 설정하여 로그를 수집할 수 있으며 수집된 정보는 lofile 파라미터를 통해 사용자가 원하는 곳에 저장이 가능합니다.

```sh
[lena@LNJDUWS2 redis-replication]$ vi redis-master-5001.conf

# Specify the server verbosity level.
# This can be one of:
# debug (a lot of information, useful for development/testing)
# verbose (many rarely useful info, but not a mess like the debug level)
# notice (moderately verbose, what you want in production probably)
# warning (only very important / critical messages are logged)
loglevel notice

# Specify the log file name. Also the empty string can be used to force
# Redis to log on the standard output. Note that if you use standard
# output for logging but daemonize, logs will be sent to /dev/null
logfile "/engn001/redis/redis-cluster-system/redis-replication/logs/redis_master_5001.log"

# To enable logging to the system logger, just set 'syslog-enabled' to yes,
# and optionally update the other syslog parameters to suit your needs.
syslog-enabled yes          # 시스템 로그 수집 여부

# Specify the syslog identity.
syslog-ident redis-master   # 시스템 로그의 식별자


```

> 모니터링

```sh
[lena@LNJDUWS2 redis-replication]$ vi redis-master-5001.conf


# By default latency monitoring is disabled since it is mostly not needed
# if you don't have latency issues, and collecting data has a performance
# impact, that while very small, can be measured under big load. Latency
# monitoring can easily be enabled at runtime using the command
# "CONFIG SET latency-monitor-threshold <milliseconds>" if needed.
latency-monitor-threshold 25  # 25밀리케컨드 이상 소요되는 작업을 수집 분석 한다
enable-debug-command yes      # redis-cli에서 debug 명령어를 수행하기 위해 yes로 설정한다


[lena@LNJDUWS2 redis-replication]$ ./src/redis-cli -p 5001

127.0.0.1:5001> debug sleep .25
OK
127.0.0.1:5001> latency latest
1) 1) "command"
   2) (integer) 1691368790
   3) (integer) 250
   4) (integer) 250
127.0.0.1:5001> latency doctor

"Dave, I have observed latency spikes in this Redis instance. You don't mind talking about it, do you Dave?

1. command: 1 latency spikes (average 250ms, mean deviation 0ms, period 21.00 sec). Worst all time event 250ms.

I have a few advices for you:

- Check your Slow Log to understand what are the commands you are running which are too slow to execute. Please check https://redis.io/commands/slowlog for more information.
- Deleting, expiring or evicting (because of maxmemory policy) large objects is a blocking operation. If you have very large objects that are often deleted, expired, or evicted, try to fragment those objects into multiple smaller objects.
- I detected a non zero amount of anonymous huge pages used by your process. This creates very serious latency events in different conditions, especially when Redis is persisting on disk. To disable THP support use the command 'echo never > /sys/kernel/mm/transparent_hugepage/enabled', make sure to also add it into /etc/rc.local so that the command will be executed again after a reboot. Note that even if you have already disabled THP, you still need to restart the Redis process to get rid of the huge pages already created."

127.0.0.1:5001> exit


[lena@LNJDUWS2 redis-replication]$ ./src/redis-cli -p 5001 --latency
min: 0, max: 1, avg: 0.20 (1242 samples)

[lena@LNJDUWS2 redis-replication]$ ./src/redis-cli -p 5001 --latency-history
min: 0, max: 1, avg: 0.15 (1461 samples) -- 15.00 seconds range
min: 0, max: 1, avg: 0.12 (1462 samples) -- 15.01 seconds range

[lena@LNJDUWS2 redis-replication]$ ./src/redis-cli -p 5001 --bigkeys

# Scanning the entire keyspace to find biggest keys as well as
# average sizes per key type.  You can use -i 0.1 to sleep 0.1 sec
# per 100 SCAN commands (not usually needed).

[00.00%] Biggest string found so far '"redis"' with 4 bytes
[00.00%] Biggest hash   found so far '"4470CB83DD6E5F6C2CF1CAFDEFBD3A8E"' with 2 fields
[00.00%] Biggest string found so far '"jvmRoute"' with 17 bytes

-------- summary -------

Sampled 6 keys in the keyspace!
Total key length in bytes is 55 (avg len 9.17)

Biggest   hash found '"4470CB83DD6E5F6C2CF1CAFDEFBD3A8E"' has 2 fields
Biggest string found '"jvmRoute"' has 17 bytes

0 lists with 0 items (00.00% of keys, avg size 0.00)
1 hashs with 2 fields (16.67% of keys, avg size 2.00)
5 strings with 31 bytes (83.33% of keys, avg size 6.20)
0 streams with 0 entries (00.00% of keys, avg size 0.00)
0 sets with 0 members (00.00% of keys, avg size 0.00)
0 zsets with 0 members (00.00% of keys, avg size 0.00)



```

## Redis Cluster 장애 복구

### Client for Redis Server

Redis Server로 접속하여 데이터를 처리할 수 있는 클라이언트 API는 대표적으로 JEDIS, Redisson, Lettuce 3가지가 있다.
최근 트렌드는 Lettuce를 쓰는데 그 이유는 성능면에서 다른 두 API보다 앞서기 때문이다.  
아래는 spring boot 에서 Lettuce를 활용한 Sample Code이다.

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

Lettuce를 활용하기 위한 Configuration

```java
package org.lat.dooly;

import lombok.RequiredArgsConstructor;
import org.springframework.boot.autoconfigure.data.redis.RedisProperties;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.connection.RedisConnectionFactory;
import org.springframework.data.redis.connection.lettuce.LettuceConnectionFactory;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.data.redis.repository.configuration.EnableRedisRepositories;
import org.springframework.data.redis.serializer.StringRedisSerializer;

@RequiredArgsConstructor
@Configuration
@EnableRedisRepositories
public class RedisRepositoryConfig {
    private final RedisProperties redisProperties;

    // lettuce
    @Bean
    public RedisConnectionFactory redisConnectionFactory() {
        return new LettuceConnectionFactory(redisProperties.getHost(), redisProperties.getPort());
    }

    @Bean
    public RedisTemplate<String, Object> redisTemplate() {
        RedisTemplate<String, Object> redisTemplate = new RedisTemplate<>();
        redisTemplate.setConnectionFactory(redisConnectionFactory());
        redisTemplate.setKeySerializer(new StringRedisSerializer());
        redisTemplate.setValueSerializer(new StringRedisSerializer());
        return redisTemplate;
    }
}

```

application.properties

```properties
spring.redis.host=127.0.0.1
spring.redis.port=5001

# for redis cluster
spring.redis.cluster.nodes[0]=127.0.0.1:5001
spring.redis.cluster.nodes[1]=127.0.0.1:5002
spring.redis.cluster.nodes[2]=127.0.0.1:5003
```

실제 호출 소스

```java
package org.lat.dooly;


import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class RedisController {

    @Autowired
    private RedisTemplate redisTemplate;

    @GetMapping("/set")
    public String set(){
        redisTemplate.opsForValue().set("key","davidyu");
        return "success";
    }

    @GetMapping("/get")
    public String get(){
        System.out.println("redisTemplate get value => {}" + redisTemplate.opsForValue().get("key"));
        return "success";
    }
}
```
