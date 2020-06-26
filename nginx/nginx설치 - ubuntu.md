## 환경 

* Ubuntu 18.04
* nginx ver : 1.16.1

## nginx(1.16.1 ver) 설치   
```code
# apt repository 에 설치하고자 하는 nginx 버전 추가 

sudo touch /etc/apt/sources.list.d/nginx.list
echo "deb http://nginx.org/packages/ubuntu/ bionic nginx" | sudo tee -a /etc/apt/sources.list.d/nginx.list
echo "deb-src http://nginx.org/packages/ubuntu/ bionic nginx"| sudo tee -a /etc/apt/sources.list.d/nginx.list


# 인증 키 등록
wget http://nginx.org/keys/nginx_signing.key
sudo apt-key add nginx_signing.key


# 저장소 업데이트
sudo apt-get update


# nginx 설치
sudo apt-get install nginx


# nginx 버전 확인 - 1.16.1
nginx -v 

# nginx 시작하기
sudo service nginx start

#nginx 종료
sudo service nginx stop

```

http://localhost
접속해서 nginx 구동 되는지 확인
