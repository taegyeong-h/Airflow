# Repo.

*Airflow Toy Project* 

>[!Tip]
>26년 5월 기준 최신 버전인 Airflow 3.2.1 기준으로 진행하며 필요할때마다 업데이트 할 예정  


## 프로젝트 구조 및 관리 규칙  

- 소스 및 문서는 **반드시!!! 꼭!!! 기록**해 둘 것!!!!!
- 문서는 마크다운 형식으로 작성할 것.

```bash
Airlfow/
├─ backup/         # 미사용 문서 및 소스들은 이 폴더로 이관
├─ docs/
│  ├─ setup/       # 설치 및 환경설정 관련 문서
│  ├─ 접속정보.md    # 내부/외부 서비스 접속 정보
│  └─ PostgreSQL_DB정보.md  # PostgreSQL DB에 들어있는 데이터 요약정보
├─ src/
│  ├─ dags/            # Airflow DAG 소스
│     ├─ notebook/     # 파이썬 및 노트북 소스
│     └─ sql/          # DB 스키마별 DDL
└─ README.md        # 공용 리포지토리 사용가이드
```

## 개인 스터디

- 배경 및 목적  
  - DB/클라우드/AI 활용의 아이디어 구현화  
  - 프로젝트 수행 역량 향상 기대  
  - 지식의 자산화 및 기술정보 공유  
- 내용  
  - 홍태경 : Airflow 기반의 DB I/F 구현 
- 일정  
  1차 스프린트 close 타겟일자을 6월 18일로 예상.
- (예상) 산출물
    - PostgreSQL 및 MinIO(스토리지) 설치 가이드 
    - 아키텍처 구성도
  - 홍태경 
    -  Airflow 설치 및 소스 배포방법 가이드
    -  Airflow 개발환경 구성가이드
    -  DB I/F 샘플 노트북 및 Airflow DAG 소스
