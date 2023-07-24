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

## 복제 & 분산 시스템 개요

## Master & Slave & Sentinel

## 부분 동기화

## Redis Cluster 구축 및 운영

### _Redis Cluster 명령어를 이용한 수동 설정_

> 총 4대의 Redis 설치

```sh
[lena@LNJDUWS2 redis-cluster]$ ls -lrt
total 16
drwxrwxr-x. 8 lena lena 4096 Mar  1 01:32 redis-slave-5004
drwxrwxr-x. 8 lena lena 4096 Mar  1 01:32 redis-slave-5003
drwxrwxr-x. 8 lena lena 4096 Mar  1 01:32 redis-master-5002
drwxrwxr-x. 8 lena lena 4096 Mar  1 01:32 redis-master-5001
```

> redis.conf 파일 수정

```properties
port                        5001
cluster-enabled             yes
cluster-config-file         nodes-5001.conf
cluster-node-timeout        5000
dir                         ./data
appendonly                  yes
```

위 설정을 다른 3대의 서버에도 적용한다.(port는 변경)

# Redis - Tomcat Session 연동

> Redis Session Manager 다운로드

```sh
 wget https://github.com/ran-jit/tomcat-cluster-redis-session-manager/releases/download/2.0.4/tomcat-cluster-redis-session-manager.zip
```

> 압축 해제 및 library, conf 파일을 tomcat 하위 폴더로 복사

```sh
[lena@LNJDUWS2 tomcat]$ unzip tomcat-cluster-redis-session-manager.zip
[lena@LNJDUWS2 tomcat]$ cp tomcat-cluster-redis-session-manager/lib/* ./apache-tomcat-8.5.91/lib
[lena@LNJDUWS2 tomcat]$ cp tomcat-cluster-redis-session-manager/conf/* ./apache-tomcat-8.5.91/conf
[lena@LNJDUWS2 tomcat]$ cd apache-tomcat-8.5.91/conf/
[lena@LNJDUWS2 conf]$ vi redis-data-cache.properties

```

> redis-data-cache.properties 설정

```sh
#-- Redis data-cache configuration

#- redis hosts ex: 127.0.0.1:6379, 127.0.0.2:6379, 127.0.0.2:6380, ....
redis.hosts=127.0.0.1:5000

#- redis password (for stand-alone mode)
#redis.password=

#- set true to enable redis cluster mode
redis.cluster.enabled=false

#- redis database (default 0)
#redis.database=0

#- redis connection timeout (default 2000)
#redis.timeout=2000

```

> context.xml 설정

SessionHAndlerValve와 SessionManager를 추가

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!--
  Licensed to the Apache Software Foundation (ASF) under one or more
  contributor license agreements.  See the NOTICE file distributed with
  this work for additional information regarding copyright ownership.
  The ASF licenses this file to You under the Apache License, Version 2.0
  (the "License"); you may not use this file except in compliance with
  the License.  You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License.
-->
<!-- The contents of this file will be loaded for each web application -->
<Context>

    <!-- Default set of monitored resources. If one of these changes, the    -->
    <!-- web application will be reloaded.                                   -->
    <WatchedResource>WEB-INF/web.xml</WatchedResource>
    <WatchedResource>${catalina.base}/conf/web.xml</WatchedResource>

    <!-- Uncomment this to disable session persistence across Tomcat restarts -->
    <!--
    <Manager pathname="" />
    -->
    <Valve className="tomcat.request.session.redis.SessionHandlerValve" />
    <Manager className="tomcat.request.session.redis.SessionManager" />
</Context>

```

> session.jsp 를 tomcat에 배포

아래 jsp 는 sample이다.

```jsp
<%@page contentType="text/html; charset=UTF-8"%>
<%@ page import="java.text.*"%>
<%@ page import="java.util.*"%>
<%
  String RsessionId = request.getRequestedSessionId();
  String sessionId = session.getId();
  boolean isNew = session.isNew();
  long creationTime = session.getCreationTime();
  long lastAccessedTime = session.getLastAccessedTime();
  int maxInactiveInterval = session.getMaxInactiveInterval();
  Enumeration e = session.getAttributeNames();
%>
<html>
 <head>
  <meta http-equiv="Content-Type" content="text/html; charset=EUC-KR">
   <title>Session Test</title>
 </head>
 <body>
    <table border=1 bordercolor="gray" cellspacing=1 cellpadding=0 width="100%">
      <tr bgcolor="gray">
       <td colspan=2 align="center"><font color="white"><b>Session Info</b></font></td>
      </tr>
     <tr>
       <td>Server HostName</td>
       <td><%=java.net.InetAddress.getLocalHost().getHostName()%></td>
     </tr>
     <tr>
       <td>Server IP</td>
       <td><%=java.net.InetAddress.getLocalHost().getHostAddress()%></td>
     </tr>
     <tr>
       <td>Request SessionID</td>
       <td><%=RsessionId%></td>
     </tr>
     <tr>
       <td>SessionID</td>
       <td><%=sessionId%></td>
     </tr>
     <tr>
       <td>isNew</td>
       <td><%=isNew%></td>
     </tr>
     <tr>
       <td>Creation Time</td>
       <td><%=new Date(creationTime)%></td>
     </tr>
     <tr>
       <td>Last Accessed Time</td>
       <td><%=new Date(lastAccessedTime)%></td>
     </tr>
     <tr>
       <td>Max Inactive Interval (second)</td>
       <td><%=maxInactiveInterval%></td>
     </tr>
     <tr bgcolor="cyan">
       <td colspan=2 align="center"><b>Session Value List</b></td>
     </tr>
     <tr>
       <td align="center">NAME</td>
      <td align="center">VAULE</td>
     </tr>
<%
 String name = null;
 while (e.hasMoreElements()) {
 name = (String) e.nextElement();
%>
    <tr>
       <td align="left"><%=name%></td>
       <td align="left"><%=session.getAttribute(name)%></td>
     </tr>
<%
 }
%>
</table>
<%
 int count = 0;
 if(session.getAttribute("count") != null)
 count = (Integer) session.getAttribute("count");
 count += 1;
 session.setAttribute("count", count);
 out.println(session.getId() + " : " + count);
%>
  </body>
</html>
```
