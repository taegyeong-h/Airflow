
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
airflow db migrate

# 2. 에어플로우 공장 가동하기 (종합 선물 세트 콤보 기동)
airflow standalone
