
### 01-init.ubuntu26.init.md postgresql 설치 및 셋업 이후 진행
```
# Airflow.cfg 설정

[database] 
- airflow ➔ 원격 DB에 생성한 계정명
- airflow_pass ➔ 원격 DB 계정의 패스워드
- airflow-rds-instance....amazonaws.com ➔ AWS가 발급해 준 원격 호스트 주소(Host Name)
- 5432 ➔ 원격 PostgreSQL이 열어둔 원격 포트(Port)
- airflow_prod ➔ 그 원격 DB 안에 파놓은 에어플로우 전용 데이터베이스 이름

#sql_alchemy_conn = sqlite://home/ubuntu/airflow/airflow.db
#sql_alchemy_conn = postgresql+psycopg2://airflow:airflow_pass@airflow-rds-instance.c123456789.ap-northeast-2.rds.amazonaws.com:5432/airflow_prod
sql_alchemy_conn = postgresql+psycopg2://airflow:airflow@localhost:5432/airflow


[core]
# SQLite 전용 일렬종대 지휘관 해고
# executor = SequentialExecutor

# 포스트그레스 전용 멀티 워커 병렬 지휘관 임명!
executor = LocalExecutor
```

# 1. 새 장부(PostgreSQL)에 에어플로우 전용 메타 테이블들 붓기 
```
airflow db migrate
2026-05-19T09:51:31.924696Z [info     ] setup plugin alembic.autogenerate.schemas [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T09:51:31.925164Z [info     ] setup plugin alembic.autogenerate.tables [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T09:51:31.925308Z [info     ] setup plugin alembic.autogenerate.types [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T09:51:31.926031Z [info     ] setup plugin alembic.autogenerate.constraints [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T09:51:31.926235Z [info     ] setup plugin alembic.autogenerate.defaults [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T09:51:31.926377Z [info     ] setup plugin alembic.autogenerate.comments [alembic.runtime.plugins] loc=plugins.py:37
2026-05-19T09:51:32.466067Z [info     ] Performing upgrade to the metadata database [airflow.cli.commands.db_command] loc=db_command.py:134 url=postgresql+psycopg2://airflow:***@localh              ost:5432/airflow
2026-05-19T09:51:32.473855Z [info     ] Context impl PostgresqlImpl.   [alembic.runtime.migration] loc=migration.py:210
2026-05-19T09:51:32.474221Z [info     ] Will assume transactional DDL. [alembic.runtime.migration] loc=migration.py:213
2026-05-19T09:51:32.669713Z [info     ] Context impl PostgresqlImpl.   [alembic.runtime.migration] loc=migration.py:210
2026-05-19T09:51:32.670122Z [info     ] Will assume transactional DDL. [alembic.runtime.migration] loc=migration.py:213
2026-05-19T09:51:32.689184Z [info     ] Creating Airflow database tables from the ORM [airflow.utils.db] loc=db.py:739
2026-05-19T09:51:32.689450Z [info     ] Creating global lock context   [airflow.utils.db] loc=db.py:720
2026-05-19T09:51:32.704297Z [info     ] Pool status: Pool size: 5  Connections in pool: 0 Current Overflow: -3 Current Checked out connections: 2 [airflow.utils.db] loc=db.py:723
2026-05-19T09:51:32.704470Z [info     ] Creating metadata              [airflow.utils.db] loc=db.py:725
2026-05-19T09:51:33.001322Z [info     ] Getting alembic config         [airflow.utils.db] loc=db.py:728
2026-05-19T09:51:33.003438Z [info     ] Stamping migration head        [airflow.utils.db] loc=db.py:731
2026-05-19T09:51:33.007600Z [info     ] Context impl PostgresqlImpl.   [alembic.runtime.migration] loc=migration.py:210
2026-05-19T09:51:33.008295Z [info     ] Will assume transactional DDL. [alembic.runtime.migration] loc=migration.py:213
2026-05-19T09:51:33.038873Z [info     ] Running stamp_revision  -> 1d6611b6ab7c [alembic.runtime.migration] loc=migration.py:621
2026-05-19T09:51:33.051231Z [info     ] Airflow database tables created [airflow.utils.db] loc=db.py:734
2026-05-19T09:51:33.191018Z [info     ] Database migration done!       [airflow.cli.commands.db_command] loc=db_command.py:152


```
# 2. 에어플로우 공장 가동하기 (종합 선물 세트 콤보 기동)
airflow standalone

