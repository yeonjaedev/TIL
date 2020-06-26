## 0. postgresql 외부 접속 허용  

(했다는 가정하에 아래 진행)

[참고]
https://m.blog.naver.com/PostView.nhn?blogId=ships95&logNo=220237438650&proxyReferer=https:%2F%2Fwww.google.com%2F


## 1. /opt/wildfly/modules 밑에 /org/postgresql/main 디렉토리 생성

## 2. 생성된 디레고리(main)안에 postgresql jdbc 4.2 driver 42.2.12 다운

`wget https://jdbc.postgresql.org/download/postgresql-42.2.12.jar`

안되는 경우) ifup으로 NAT에 연결후 다운 진행

## 3. main 디렉토리 안에 module.xml 생성 후 아래 내용 작성

```
<?xml version="1.0" encoding="UTF-8"?>
    <module xmlns="urn:jboss:module:1.0" name="org.postgresql">
        <resources>
            <resource-root path="postgresql-42.2.12.jar"/>
        </resources>
        <dependencies>
            <module name="javax.api"/>
            <module name="javax.transaction.api"/>
        </dependencies>
    </module>
```
![module_xml](uploads/29798b1b75e61ab9e426ef7a3c1c4b00/module_xml.png)

## 4. /opt/wildfly/standalone/configuration/standalone.xml

```
<datasource jndi-name="java:jboss/datasources/PostgresDS" pool-name="PostgresDS">
    <connection-url>jdbc:postgresql://[postgresql ip 주소]:5432/[table 이름]</connection-url>
    <driver-class>org.postgresql.Driver</driver-class>
    <driver>postgresql-jdbc4</driver>
    <security>
        <user-name>[DB user 이름]</user-name>
        <password>[DB password]</password>
    </security>
    <validation>
        <check-valid-connection-sql>SELECT * FROM [table 이름]</check-valid-connection-sql>
    </validation>
</datasource>
<drivers>
    <driver name="postgresql-jdbc4" module="org.postgresql"/>
</drivers>
```
![standalone_xml](uploads/5e7f87bd19877eb08fa0d2bfcee997a5/standalone_xml.png)

## 5. wildfly 실행 
`systemctl restart wildfly`

## 6. wildfly 상태 확인
`systemctl status wildfly`

![status](uploads/e54677585a728f0a8e3894e4ab033c27/status.png)

## 7. wildfly 접속 확인

wildflyip:8080 했을때 wildfly 화면 뜨면 성공

## 8. WildFly Administration Console 접근

참고 (https://linuxize.com/post/how-to-install-wildfly-on-centos-7/)

### 8.1 jboss-cli.sh 실행
`cd /opt/wildfly/bin/`

`./jboss-cli.sh --connect`

![connect](uploads/5b6e8a5211a190e02c0d901d70b71b9b/connect.png)

이렇게 뜨면 성공, ctrl+c로 나가기

### 8.2 admin 접속

[wildflyip]:9990/console 접속

안된다면 8.3 이어서 하기

### 8.3 /etc/wildfly/wildfly.conf 수정

```
# The configuration you want to run
WILDFLY_CONFIG=standalone.xml

# The mode you want to run
WILDFLY_MODE=standalone

# The address to bind to
WILDFLY_BIND=0.0.0.0

# The address console to bind to
WILDFLY_CONSOLE_BIND=0.0.0.0
```

### /opt/wildfly/bin/launch.sh 수정
```
#!/bin/bash

if [ "x$WILDFLY_HOME" = "x" ]; then
    WILDFLY_HOME="/opt/wildfly"
fi

if [[ "$1" == "domain" ]]; then
    $WILDFLY_HOME/bin/domain.sh -c $2 -b $3 -bmanagement $4
else
    $WILDFLY_HOME/bin/standalone.sh -c $2 -b $3 -bmanagement $4
fi
```

wildfly 재시작
`systemctl restart wildfly`

`systemctl status wildfly`

wildfly 연결 확인 (fail이면 오타 확인)

### 8.4 /etc/systemd/system/wildfly.service 수정

```
[Unit]
Description=The WildFly Application Server
After=syslog.target network.target
Before=httpd.service

[Service]
Environment=LAUNCH_JBOSS_IN_BACKGROUND=1
EnvironmentFile=-/etc/wildfly/wildfly.conf
User=wildfly
LimitNOFILE=102642
PIDFile=/var/run/wildfly/wildfly.pid
ExecStart=/opt/wildfly/bin/launch.sh $WILDFLY_MODE $WILDFLY_CONFIG $WILDFLY_BIND $WILDFLY_CONSOLE_BIND
StandardOutput=null

[Install]
WantedBy=multi-user.target
```

### 8.5 permission 설정

`mkdir /var/run/wildfly/`

`chown wildfly: /var/run/wildfly/`

`systemctl daemon-reload`

`systemctl restart wildfly`

### 8.6 admin page 확인

![admin](uploads/ee2444c4e3e9fd3eef4f9a32fd35ea7b/admin.png)

### 8.7 datasource connection 확인

configuration > subsystems > Datasources&Drivers > Datasources > PostgreDS 

view 옆에 화살 표 누르고 Test Connection했을때 Success뜨면 성공
