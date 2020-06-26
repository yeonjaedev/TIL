# virtual box를 활용한 nginx 설치



### 1. CentOS 7를 탑재한 Virtual Machine을 준비

### 2. nginx 저장소를 추가

sudo vi /etc/yum.repos.d/nginx.repo

 nginx.repo

[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/7/$basearch/
gpgcheck=0
enabled=1

### 3. 제대로 반영이 되었는지 yum info를 통해 확인

yum info nginx

### 4. 설치

yum install nginx

### 5. 부팅 시 자동 구동하도록 설정

CentOS 7

systemctl enable nginx
systemctl restart nginx
