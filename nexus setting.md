## 사전작업 (방화벽)
**VM 환경** 경우, `Host IP Address -> 10.217.65.18:8081` 방화벽 작업 완료 (**newDEAL Nexus**)  
> 보통 외부 방화벽이 차단되어 있어, nexus 연동을 통해 패키지 설치 

## Nexus Repository 추가(/etc/yum.repos.d/nexus.repo)

### 1. Local에 Nexus Repository 추가 후 nexus.repo 작성
```shell
$ mkdir /etc/yum.repos.d
$ vi nexus.repo
```

* 프로젝트 계정을 통해 발급받은 nexus.repo 를 아래와 같이 사용 가능합니다.
* <project_id> : new DEAL 프로젝트 계정 ID (ex. sw-common)
* <project_pw> : new DEAL 프로젝트 계정 Password (ex. 1234)

```
[nexusrepo]
name=Nexus Repository
baseurl=http://10.217.65.18:8081/repository/yum-sw-proxy/$releasever/os/$basearch/
username=<project_id>
password=<project_pw>
enabled=1
gpgcheck=0
priority=1

[nexusrepoextras]
name=CentOS-$releasever - Extras
baseurl=http://10.217.65.18:8081/repository/yum-sw-proxy/$releasever/extras/$basearch/
username=<project_id>
password=<project_pw>
gpgcheck=0
```

### 2. nexus.repo를 VM에 copy

```shell
$ scp nexus.repo SECUSER@<VM Private IP address>:/home/SECUSER
$ ssh SECUSER@<VM Private IP address>
...
$ sudo cp nexus.repo /etc/yum.repos.d
```
### 3. /etc/yum.repos.d/CentOS-Base.repo 파일명 변경
> 이미 생성된 CentOS-Base.repo를 사용하지 않기 위함. 사실 repo_org 필요없음 

```shell
$ mv CentOS-Base.repo CentOS-Base.repo_org
```

### 4 yum update

```shell
$ sudo yum update -y
```

### 5. CentOS-Base.repo 비활성화

```
[base]
...
enabled=0
...
#released updates 
[updates]
...
enabled=0
...

#additional packages that may be useful
[extras]
...
enabled=0
...

#additional packages that extend functionality of existing packages
[centosplus]
...
enabled=0
...
``` 
