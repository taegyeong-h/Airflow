# PostgreSQL 설치 가이드

> [!Note]
> VirtualBox Ubuntu 26.04 환경 기준. ( [VirtualBox 설치 가이드](VirtualBox_설치가이드.md) 문서 참고 )

## PostgreSQL 설치
1. PostgreSQL 설치
    ```bash
    sudo apt install postgresql 
    ```
2. PostgreSQL 접속
    ```bash
    sudo -i -u postgres
    psql
    ```
3. DB 유저 생성  
    ```sql
    postgres=# create user 아이디 password '비밀번호' superuser;
    postgres=# \du
    quit
    ```
4. 외부 접속 설정
    ```bash
    nano /etc/postgresql/18/main/postgresql.conf
    ```
    `CONNECTIONS AND AUTHENTICATION` 항목에서, `listen_addresses = '*'` 로 변경  
    ```ini
    #--------------------------------------
    # CONNECTIONS AND AUTHENTICATION
    #--------------------------------------

    # - Connection Settings -

    listen_addresses = '*'    # what IP address(es) to listen on;
    ```
    ```bash
    nano /etc/postgresql/18/main/pg_hba.conf
    ```
    `IPv4 local connections` 에서 host의 ADDRESS를 `0.0.0.0/0`으로 변경
    ```ini
    # IPv4 local connections:
    host    all             all             0.0.0.0/0            scram-sha-256
    ```
5. PostgreSQL 재시작
    ```bash
    # postgres 계정 로그아웃
    exit

    sudo service postgresql restart
    ```

## (선택사항) pgAdmin4 설치 
```bash
curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo gpg --dearmor -o /usr/share/keyrings/packages-pgadmin-org.gpg

sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'

# gpg 명령어 오류 발생하는 경우, gnupg 패키지 설치.
sudo apt install gnupg

# 데스크톱과 웹 모드 모두에 설치:
sudo apt install pgadmin4
# 데스크톱 모드로만 설치:
sudo apt install pgadmin4-desktop
# 웹 모드에만 설치:
sudo apt install pgadmin4-web

# pgadmin4-web을 설치한 경우 웹 서버를 구성
sudo /usr/pgadmin4/bin/setup-web.sh
```

> [!Tip]
> pgAdmin4 화면에서 한글이 깨질 시,  
> 화면의 왼쪽 `Object Explorer`에서 해당 서버를 우클릭 > `Properties` > `Parameters`  
> Connection Parameter에 `client_encoding` : `UTF8` 추가.

## (선택사항) Timescale DB 설치 

> [!Warning]
> I/O 부하 이슈가 있으니, 사전에 잘 검토해 볼 것!!

```bash
# 1. 패키지 저장소 스크립트 실행
curl -s https://packagecloud.io/install/repositories/timescale/timescaledb/script.deb.sh | sudo bash

# 2. 패키지 목록 업데이트
sudo apt update

# 3. Postgres 버전 확인
psql --version

# 4. Postgres 버전에 맞는 패키지 설치 (현 운용버전 = 16)
sudo apt install timescaledb-2-postgresql-16

# 5. postgres 성능을 위한 메모리 및 라이브러리 설정 변경
# timescaledb-tune을 이용하여 자동 메모리 관리 설정
# 모든 질문사항에 대해 y를 입력하여 진행
sudo timescaledb-tune

# 6. 특정 데이터베이스에 TimescaleDB 활성화
sudo -u postgres psql -d shko_db
CREATE EXTENSION IF NOT EXISTS timescaledb;
\q
```
