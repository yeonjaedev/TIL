
## 1. PostgreSQL 설치하기!
편집
```
sudo yum install -y postgresql
```
이렇게 설치를 시도하면 postgresql 의 9.x버전이 설치됩니다!

( -y 옵션은 중간에 나오는 y/n 물음을 전부 yes로 진행하겠다는 것입니다. )

## 2. PostgreSQL-server 설치하기!
편집
현재 postgresql의 버전은 9.x 버전인데 반해 postgresql-server의 버전은 11 버전이라 실행 시 오류가 발생할 수도 있다는 경고가 출력됩니다.

그래서 11버전을 설치하고 싶으신 분들이 있다면!
```
sudo rpm -Uvh https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```
을 통해 repository를 설치해주시기 바랍니다.

-U 옵션은 패키지를 업그레이드하는 옵션입니다.

-v 는 자세히 정보를 출력하는 옵션

-h는 자세한 설치로그를 #문자를 사용해 출력해주는 옵션입니다.
```
sudo yum install -y postgresql11-server postgresql11-contrib
```
이렇게 postgresql server를 11버전으로 설치할 수 있습니다. 

위의 명령어는 2가지를 설치하는데요 emoticon_smile

postgresql11-server : DB 서버
postgresql11-contrib : 추가적으로 필요한 모듈
이렇게 2가지를 한번에 설치합니다.

여기까지 postgresql과 DB서버의 설치를 마쳤습니다!! 

## 3. 기본 Database 생성하기!
편집
이제 DB서버가 설치되었으므로 기본 DB를 설치합니다.
```
sudo /usr/pgsql-11/bin/postgresql-11-setup initdb
```
위 initdb라는 명령어를 통해 기본 DB가 설치되며 이를 통해 생성된 DB는 기본적으로 postgres라는 이름을 갖게 됩니다.

## 4. PostgreSQL 실행하기~
편집
```
sudo systemctl start postgresql-11
sudo systemctl enable postgresql-11
```
위 명령어를 통해 DB서비스를 실행하고 등록하게 됩니다.

현재까지 PostgreSQL을 설치하고 실행하는 것까지 해보았습니다.

곧 외부에서 DB와 연동하는 법을 찾아 업로드하도록 하겠습니다.

감사합니다! 좋은 하루되세요!!!🤗

------------------------------------------------------------------------------------------------

참고 : https://medium.com/@jinseok.choi/centos-7%EC%97%90%EC%84%9C-postgresql-11-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0-77bc0da9d0af
