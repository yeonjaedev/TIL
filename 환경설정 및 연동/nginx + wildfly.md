​
# Proxy를 이용한 Nginx와 Wildfly 연동 및 이중화
1.네트워크 설정을 해줘야 한다. <br>
2.Nginx VM과 Wildfly VM을 준비힌다.<br>
3.두 VM간의 통신을 위해, 로컬에서 접속할 수 있는 IP를 자동으로 부여받아야 한다. -> Virtual Box 메뉴 '도구'에서  네트워크를 선택한다.<br>
4.'만들기'를 눌러 새로운 네트워크가 생성됨을 볼 수 있다.<br>
​​
5.Nginx, Wildfly VM 각각의 설정에 들어가서 네트워크 메뉴에서  어댑터 1은 NAT에 연결,<br>
6.어댑터2는 '다음에 연걸됨' 을 '호스트 전용 어댑터'로 변경한다. 이때, 어떤 네트워크가 '이름'에 할당돼있는 것을 볼 수 있다.<br>
(그림은 어댑터1이 호스트지만 어댑터2가 호스트로 가게 해주세요.)<br>
7.Nginx, Wildfly VM에 각각 접속하여 ip addr와 ifup 명령어를 통해 다른 문서의 기본 설정처럼 네트워크에 연결한다.<br>
8.각각 VM에 다시 ip addr 명령어를 친다.<br>
9.2번 enp0s3 밑에 , inet 오른쪽에 192로 시작하는 ip가 부여된것을 볼 수 있다. 그 ip가 해당되는 VM의 ip 주소이다.<br>

10.해당 ip를 기억하고, 다음으로 Nginx VM에서 프록시를 설정해주어야 한다.<br>
11.다음의 경로로 들어가 /etc/nginx/conf.d    default.conf를 연다.<br>
12.다음과 같이 wildfly upstream을 열어주고 그 안에 Wildfly VM의 IP를 넣어준다.  (이름은 자유) , server 내에 location /wildfly 를 새로 작성해준다.<br>
 (wildfly upstream 내부에 ip가 2개 있는데, 저 2개의 ip는 2개의 Wildfly VM의 각각의 ip로써, 저렇게 설정해줌으로써 이중화를 해주는 것이다. Nginx에서 2개의 wildfly로 자동으로 로드밸런싱을 해주는 것이다. )<br>
13.저정하고 나간뒤 nginx -t 를 통해 conf파일에 syntax에러가 없는지 확인한다.<br>
14.systemctl restart nginx로 nginx서버를 다시 실행해준다.<br>
15.Ubuntu 크롬 브라우저에서 http://[nginxIP]/wildfly 를 입력해 wildfly IndexPage가 뜨는 것을 확인하면 성공한 것이다.<br>

* 기타 ISSUE
안될 경우, setsebool name_tcp_bind_http_port on 와 setsebool httpd_can_network_connect on 를 터미널에 입력하여 적용시켜주고 다시 해본다. <br>
Proxy default.conf를 작성할때 proxy pass 뒷부분에 /를 빼먹지 말것.
 



​
