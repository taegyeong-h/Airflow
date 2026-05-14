## 1. Ubuntu 22.04 In Virtualbox

- ubuntu incloude in sudo group  -- 최초 로그인 시 ubuntu 일반 유저도 sudo 명령어를 사용하기 위해서는 sudo group 에 ubuntu 계정을 넣어줘야한다  
  - su -        -- root 계정 로그인 (password 입력 프롬프트 뒤에 "$" -> "#" 확인)   
  - root@ubuntu:#  sudo usermod -aG sudo ubuntu   -- ubuntu 일반 계정에 sudo Group 에 포함시켜 sudo 사용권한을 가진다  
  - su ubuntu           -- root 계정에서 ubuntu 일반 계정으로 전환 (마찬가지로 프롬프트 뒤에 "#" -> "$" 확인) 
  - ubuntu@ubuntu:/root$ cd        
  - ubuntu@ubuntu:~$              -- ubuntu 홈 디렉토리 에서 작업 시작

- packege list Update & Upgrade
  - sudo apt update && sudo apt upgrade -y

- took install (Network check, Text editor, Distributed Shell
  - sudo apt install -y net-tools vim openssh-server pip

- python 3.11 install  
  - DeadSnakes PPA 저장소 추가 및 설치   -- (default Python 3.10) Python 3.11을 설치하려면 deadsnakes PPA 저장소를 사용하는 것이 가장 일반적이고 권장
    - sudo add-apt-repository ppa:deadsnakes/ppa -y
    - sudo apt update
    - sudo apt install python3.11 python3.11-venv python3.11-dev -y
    - python 3.11 --version
      - python 3.11.15 -- 3.11.15 버전 확인 

- airflow_venv'라는 이름의 3.11 전용 방(폴더) 만들기 -- 위에서도 말했지만 Ubuntu 22.04 default python 3.10 이라 3.11 전용 방을 만들어아 햠 
  - python3.11 -m venv ~/airflow_venv

- 그 방으로 들어가기 (활성화)
  - source ~/airflow_venv/bin/activate
  - (airflow_venv) ubuntu@ubuntu:~$
  - pip install --upgrade pip
  - pip 24.0 -> 26.1.1 

export AIRFLOW_HOME=~/airflow    -- "너의 모든 설정 파일, 로그, 데이터베이스 파일은 이 폴더(~/airflow)에 저장하고 관리해!"라고 '집 주소'를 알려주는 것 same "JAVA_HOME"
(airflow_venv) ubuntu@ubuntu:~$ echo "export AIRFLOW_HOME=~/airflow" >> ~/.bashrc

tail -1 ~/.bashrc               -- bashrc 편집기 마지막 줄 확인
export AIRFLOW_HOME=~/airflow   

