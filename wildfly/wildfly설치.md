# 로컬환경(ubuntu)에서 wildfly 설치


### 1. 최신버전으로 업데이트
```
$ sudo apt-get update
```


### 2. openjdk 버전 확인
```
$ java -version
#openjdk version "1.8.0_242" 확인
```


### 3. 시스템 사용자 만들기  
WildFly를 루트 사용자로 실행하지 않는 것이 좋음 따라서 새 시스템 사용자를 생성하여 사용  
'wildfly'시스템 사용자 및 그룹을 생성  
```
$ sudo groupadd -r wildfly
$ sudo useradd -r -g wildfly -d /opt/wildfly -s /sbin/nologin wildfly
```


### 4. 버전 명시 후 설치파일 다운로드
```
$ Version_Number=19.0.0.Final
$ wget https://download.jboss.org/wildfly/$Version_Number/wildfly-$Version_Number.tar.gz -P /tmp
```


### 5. /opt/에 압축풀기
```
$ sudo tar xf /tmp/wildfly-$Version_Number.tar.gz -C /opt/
```


## 6. 심볼릭 링크를 생성
이 링크는 WildFly 설치 디렉토리를 가리킴
```
$ sudo ln -s /opt/wildfly-$Version_Number /opt/wildfly
```


### 7. 권한 부여
```
$ sudo chown -RH wildfly: /opt/wildfly
```

### 8. 서비스로 실행되도록 환경설정
#### 8-1. wildfly.conf 파일을 복사 할 디렉토리를 생성
```
$ sudo mkdir -p /etc/wildfly
```
#### 8-2. 생성한 디렉토리로 복사
``` 
$ sudo cp /opt/wildfly/docs/contrib/scripts/systemd/wildfly.conf /etc/wildfly/
```
#### 8-3. 수정
```
$ sudo nano /etc/wildfly/wildfly.conf
```
{{image.png}}
확인

#### 8-4. launch.sh 파일 복사
```
$ sudo cp /opt/wildfly/docs/contrib/scripts/systemd/launch.sh /opt/wildfly/bin/
$ sudo sh -c 'chmod +x /opt/wildfly/bin/*.sh'

```

#### 8-5. wildfly.service 파일 복사
```
$ sudo cp /opt/wildfly/docs/contrib/scripts/systemd/wildfly.service /etc/systemd/system/
```
#### 8-6. daemon reload
```
$ sudo systemctl daemon-reload
```

### 9. wildfly 서비스 시작

```
$ sudo systemctl start wildfly
$ sudo systemctl status wildfly
$ sudo systemctl enable wildfly
```



# WildFly 구성
WildFly를 설치하고 서비스로 실행 했으므로 이제 몇 가지 구성을 해야 함

* 방화벽 조정
* 안전한 WildFly 관리자 생성
* 성공적인 설정 확인
* 로컬 및 원격으로 WildFly 관리 콘솔에 액세스

### 1. 포트 8080에서 트래픽 허용
```
$ sudo ufw allow 8080/tcp
```

### 2. wildfly 관리자 생성
```
$ sudo /opt/wildfly/bin/add-user.sh
```
a
username : santa
password : 1234
y
y
y
입력

### 3. 성공적인 설정 확인하기
http://<your_domain_or_IP_address>:8080 접속  

localhost:8080

### 4. 관리자 콘솔 확인하기  

http://localhost:9990/console 접속  


참조링크 : Install and Configure Wildfly (JBoss) on Ubuntu 18.04 LTS (https://vitux.com/install-and-configure-wildfly-jboss-on-ubuntu/)_
