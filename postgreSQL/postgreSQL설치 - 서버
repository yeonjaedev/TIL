## 1. postgresql.repo 추가(/etc/yum.repos.d)

```shell
cd /etc/yum.repos.d
vi postgresql.repo
```

  * 설치 시 nexus 에 설정된 Repository 의 remote URL 확인 필수
  * 아래는 `12` 버전

```
[postgresqlrepo]
name=Nexus Repository - PostgreSQL
baseurl=http://sw-common:1234@10.217.65.18:8081/repository/yum-sw-postgresql-proxy/12/redhat/rhel-$releasever-$basearch/
username=sw-common
password=1234
enabled=1
gpgcheck=0
```

## 2. Repository List 확인

```shell
$ yum repolist
$ yum list | grep postgres
```

## 3. Postgresql Install

```shell
$ sudo yum install -y postgresql12 postgresql12-server postgresql12-contrib
```

## 4. DB 초기화(권한이 없는 경우, sudo)

```shell
$ /usr/pgsql-12/bin/postgresql12-setup initdb
```
## 5. conf 설정
* conf 설정(/var/lib/pgsql/12/data/pg_hba.conf)

```conf
...
host    all             all             0.0.0.0/0               password
```

* conf 설정(/var/lib/pgsql/12/data/postgresql.conf)

```conf
...
listen_addresses = '*'
```

## 6. 서비스 등록 및 시작

```shell
$ systemctl enable postgresql-9.6
$ systemctl start postgresql-9.6
```

## 7. DB 연결

```shell
sudo -u postgres psql
```

### 8. 계정 생성 및 DB 생성
[참고](https://browndwarf.tistory.com/3)
