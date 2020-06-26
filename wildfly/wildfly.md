# wildfly 설치 및 설정

* 가상 환경 스펙

Ubuntu 18.04

Virtual Box ver : 5.2.34

CentOS ver : 7.7

Wildfly ver : 19.0.0 Final

2 Core / RAM 4GB / Disk 50GB

* CentOS 7 Virtual Machine 구축 방법

1. Virtual Box 5.2.34 구동

2. CentOS 7.0.14 minimal 버전 iso 다운 (64bit)  -> http://data.aonenetworks.kr/os/CentOS/7.7.1908/isos/x86_64/

3. Virtual Box에서 Virtual Machine 새로 생성해서 Redhat 64bit / RAM 4GB / 저장소 50GB 설정 후 VM 시작

4. 2번에서 다운 받은 이미지 삽입 후 install CentOS7 - 한글/영어 설정 - root 비밀번호 설정 1234 - 계정 생성 (Santa/1234)

5. 기다리면 자동으로 CentOS가 Reboot되고 터미널이 뜨며, 5번에서 설정한 게정으로 로그인하면 초기 설정 끝

* Virtual Machine Network 설정

1. 네트워크 연결을 위해 터미널에 ip addr 입력하면 연결 가능한 네트워크 옵션들이 나열된다.   $ ip addr

2. 나열된 옵션들 중 2번째 네트워크인 enp0s3으로 설정하려면 -> $ ifup enp0s3      * 만약 cannot control this device가 뜬다면 su root로 root 전환후 다시 시도하면 된다.

3. Connection Successfully 뜨면 ping google.com 명령어로 핑이 뜨는지 확인!

4. yum -y update 로 패키지 업데이트 해준다. 시간좀 걸리는거 같다.

* VM Wildfly

1.  Wildfly 19.0.0.Final  tar.gz 파일을 다운 2번으로 가세요.  ※로컬에서 다운 받지마세요. 

2. VM Centos 내에서 다운받아야 하므로 터미널에 $ wget https://download.jboss.org/wildfly/19.0.0.Final/wildfly-19.0.0.Final.tar.gz -P /tmp  입력해서 다운 (/tmp 폴더 안에 다운받기)   ※ wget이 안된다면 $ yum install wget

3. jdk 1.8.0 설치등 나머지 Wildfly에 관한 가이드는 https://linuxize.com/post/how-to-install-wildfly-on-centos-7/ 에서 따라가면 된다. ※버전 19.0.0인걸 참고. 

4. Wildfly 돌아가는지 확인은 기타 issue 1번을 통해 확인.

* 기타 Issue

1. CentOS minimal 버전에서는 웹 브라우저 기능을 제공하지 않으므로, w3m / Lynx을 설치하여 텍스트로 브라우저를 대체할 수 있다.

     -apt-get install w3m

     -yum install lynx



설치 후 확인하는 방법은??

# lynx로 브라우저 호출
$ lynx https://ip or domain_name

# 브라우저 호출'만' 하고 싶을 때 (결과만 출력해쥼)
$ lynx -dump https://ip or domain_name
