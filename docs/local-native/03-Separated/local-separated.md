

# Airflow config 셋업

```
[core]
# 1. 기존 설정 (예제 DAG 로드 활성화)
#load_examples = True

# 변경 후 설정 (예제 DAG 로드 차단)
load_examples = False

# 2. 스케줄러 실행 기준 시간대를 한국(KST)으로 변경
#default_timezone = utc
default_timezone = Asia/Seoul

# 3. 총 사령관 병행 OR 일괄 
# executor = SequentialExecutor 

# 포스트그레스 전용 멀티 워커 병렬 지휘관 임명!
executor = LocalExecutor

[api]
host = 0.0.0.0  

port = 8080

# cpu 단일 코어 하나만 사용하겠다 webai worker는 한명이면 된다
workers = 1 

# 에어플로우 시스템 전체를 통틀어 동시에(Concurrently) 실행 상태(running)로 존재할 수 있는 태스크 프로세스의 총합이 최대 32개 (리소스를 많이 잡아먹는다
#parallelism = 32
parallelism = 10

# 하나의 Dag 총 Task 16개(개당 150M 메모리 점유)
#max_active_tasks_per_dag = 16
max_active_tasks_per_dag = 10

[dag_processor]
# dags 디렉토리에 새 파일 발견은 15초 정도면 충분히 빠릅니다.
#refresh_interval = 300 
refresh_interval = 15

# dags 디렉토리에 기존 코드 수정은 10초 뒤에 반영되게 합니다.
#min_file_process_interval = 30
min_file_process_interval = 10

# guest os cpu 리소스가 4개면 3개 정도 주면 좋다 
parsing_processes = 3
```

``` bash

# airflow.cfg 이후 migrate 
airflow db migrate
```


#### airflow api-server -D ➔ 유저용 웹 화면을 보여주면서, 동시에 일꾼들의 장부 보고까지 혼자 다 처리하는 만능 매니저
```
2026-05-19T11:27:48.374902Z [info     ] setup plugin alembic.autogenerate.schemas [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T11:27:48.375374Z [info     ] setup plugin alembic.autogenerate.tables [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T11:27:48.375501Z [info     ] setup plugin alembic.autogenerate.types [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T11:27:48.375588Z [info     ] setup plugin alembic.autogenerate.constraints [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T11:27:48.375660Z [info     ] setup plugin alembic.autogenerate.defaults [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T11:27:48.375710Z [info     ] setup plugin alembic.autogenerate.comments [alembic.runtime.plugins] loc=plugins.py:37

```
#### airflow scheduler -D ➔ 시계 보면서 정해진 시간에 일꾼 로봇들을 출격시키는 깐깐한 공장장
```
  ____________       _____________
 ____    |__( )_________  __/__  /________      __
____  /| |_  /__  ___/_  /_ __  /_  __ \_ | /| / /
___  ___ |  / _  /   _  __/ _  / / /_/ /_ |/ |/ /
 _/_/  |_/_/  /_/    /_/    /_/  \____/____/|__/
(airflow_venv) ubuntu@airflow32:~/airflow_venv$ airflow scheduler -D
2026-05-19T11:27:54.594628Z [info     ] setup plugin alembic.autogenerate.schemas [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T11:27:54.595175Z [info     ] setup plugin alembic.autogenerate.tables [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T11:27:54.595892Z [info     ] setup plugin alembic.autogenerate.types [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T11:27:54.596205Z [info     ] setup plugin alembic.autogenerate.constraints [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T11:27:54.596415Z [info     ] setup plugin alembic.autogenerate.defaults [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T11:27:54.596584Z [info     ] setup plugin alembic.autogenerate.comments [alembic.runtime.plugins] loc=plugins.py:37
```
#### airflow triggerer -D ➔ 외부 대기 작업이 길어질 때 일꾼을 재우고 대신 망을 봐주는 스마트 비서
```
2026-05-19T11:28:00.471759Z [info     ] setup plugin alembic.autogenerate.schemas [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T11:28:00.472013Z [info     ] setup plugin alembic.autogenerate.tables [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T11:28:00.472131Z [info     ] setup plugin alembic.autogenerate.types [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T11:28:00.472444Z [info     ] setup plugin alembic.autogenerate.constraints [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T11:28:00.473472Z [info     ] setup plugin alembic.autogenerate.defaults [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T11:28:00.473733Z [info     ] setup plugin alembic.autogenerate.comments [alembic.runtime.plugins] loc=plugins.py:37
  ____________       _____________
 ____    |__( )_________  __/__  /________      __
____  /| |_  /__  ___/_  /_ __  /_  __ \_ | /| / /
___  ___ |  / _  /   _  __/ _  / / /_/ /_ |/ |/ /
 _/_/  |_/_/  /_/    /_/    /_/  \____/____/|__/

```
#### airflow dag-processor -D ➔ dag 코드가 수정될 때마다 실시간으로 싹 읽어서 스케줄러와 UI에 대령하는 열일하는 파서(Parser)
```
2026-05-19T11:28:00.471759Z [info     ] setup plugin alembic.autogenerate.schemas [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T11:28:00.472013Z [info     ] setup plugin alembic.autogenerate.tables [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T11:28:00.472131Z [info     ] setup plugin alembic.autogenerate.types [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T11:28:00.472444Z [info     ] setup plugin alembic.autogenerate.constraints [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T11:28:00.473472Z [info     ] setup plugin alembic.autogenerate.defaults [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T11:28:00.473733Z [info     ] setup plugin alembic.autogenerate.comments [alembic.runtime.plugins] loc=plugins.py:37
  ____________       _____________
 ____    |__( )_________  __/__  /________      __
____  /| |_  /__  ___/_  /_ __  /_  __ \_ | /| / /
___  ___ |  / _  /   _  __/ _  / / /_/ /_ |/ |/ /
 _/_/  |_/_/  /_/    /_/    /_/  \____/____/|__/

```




### airflow.config 수정 시 재실행 
```
# "airflow db migrate" 는 airflow.config 에서 DB부분 수정할 때만 사용한다
# aiorflow config 에서 [x] < 부분에 아래 4개 서비스에 포함된다면 해당 서비스만 죽이고 재 실행 하면 된다 
sudo pkill -f airflow
airflow db migrate                                                 
airflow api-server -D && airflow scheduler -D && airflow triggerer -D && airflow dag-processor -D
```

```
# 에어플로우가 자동으로 생성한 무작위 문자열  
cat ~/airflow/simple_auth_manager_passwords.json.generated
{"admin": "whv4uKffU5hSPVGH"}

# 관리자 패스워드 수정 (서버 안내려도 바로 적용됌)
vim ~/airflow/simple_auth_manager_passwords.json.generated
{"admin": "admin"}
```


# WebUi 이후 수정사항 
```
WebUi 이동 후 한국어 -> 영어로 바꾸기
```
<img width="367" height="396" alt="image" src="https://github.com/user-attachments/assets/e4796857-a074-4c65-b5fc-aa0e118ec720" />

# 새로운 유저(tghong) 등록 
```
# airflow.cfg
[core]
#simple_auth_manager_users = admin:admin
simple_auth_manager_users = admin:admin,tghong:admin

# 좀비 프로세스 전멸
sudo pkill -f airflow

# 4대장 동시 리스타트
airflow api-server -D && airflow scheduler -D && airflow triggerer -D && airflow dag-processor -D

#tghong이라는 key: value가 생겼다 tghong 패스워스 변경후 Webui 재접속
(airflow_venv) ubuntu@airflow32:~$ cat airflow/simple_auth_manager_passwords.json.generated
{"admin": "admin", "tghong": "UES6gHB8SwQur3SC"}

vim airflow/simple_auth_manager_passwords.json.generated
{"admin": "admin", "tghong": "tghong"}
```
### 🏁 가동 완료 및 아키텍처 검증

위의 4가지 명령어(`api-server`, `scheduler`, `triggerer`, `dag-processor`)가 백그라운드에서 정상 가동되었다면, 겉보기에는 기존 Standalone 모드와 같은 웹 화면이 뜨지만 내부 엔진은 완전히 달라진 상태입니다.

이제 우리는 **1) 웹서버가 뻗어도 배치가 멈추지 않는 '결함 격리 환경'**을 구축했으며, **2) PostgreSQL 장부 덕분에 수많은 태스크 워커들이 충돌 없이 동시에 병렬 처리(LocalExecutor)되는 진짜 실무형 분리 인프라**를 완성한 것입니다.
