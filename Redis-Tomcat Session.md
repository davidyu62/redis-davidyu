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
