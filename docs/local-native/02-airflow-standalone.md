# 02. Airflow Standalone 구동 및 웹 UI 확인

이 단계에서는 설치 완료된 Airflow를 원클릭 `standalone` 모드로 구동하고, 웹 브라우저를 통해 관리자 화면에 접속하는 과정을 다룹니다.

---

## 1. Airflow Standalone 실행
가상환경(`airflow_venv`)이 켜진 상태에서 아래 명령어를 실행하여 에어플로우의 모든 프로세스(웹서버, 스케줄러, SQLite DB)를 한 방에 켭니다.

```bash
# 가상환경 활성화 (안 켜져 있다면 실행)
source ~/airflow_venv/bin/activate

# 에어플로우 standalone 구동
airflow standalone
```

## 2. Airflow WebUI 실행
```bash
# host OS 브라우저에서 localhost:8080 검색
```
