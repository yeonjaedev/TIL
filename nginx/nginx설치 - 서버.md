## nginx.repo 추가(/etc/yum.repos.d)

```
[nginx-repo]
name=Nexus Repository - Nginx
baseurl=http://10.217.65.18:8081/repository/yum-sw-nginx-proxy/$releasever/$basearch/
username=sw-common
password=1234
enabled=1
gpgcheck=0
```

## yum install

```shell
$ sudo yum install nginx
```

## 서비스 등록 및 시작

```shell
$ systemctl enable nginx
$ systemctl start nginx
```
