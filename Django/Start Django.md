# Django 시작하기
## 1. 가상환경 만들기
가상환경 세팅 및 가상환경 진입하기
- 프로젝트를 시작할 폴더 안에서 아래 명령어들을 입력해야 합니다.
```bash
python -m venv 가상환경폴더명

cd 가상환경폴더명
cd bin
source ./activate
```

## 2. django 설치하기
```bash
cd ..
pip install django==버전
```

## 3. django 시작하기
프로젝트를 시작할 새 폴더를 만든 다음 시작해야 함.
```bash
mkdir 새폴더
django-admin startproject config .
```