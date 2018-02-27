# Yellowid-Flask

[![No Maintenance Intended](http://unmaintained.tech/badge.svg)](http://unmaintained.tech/)

[Unmaintained] Skeleton of Kakaotalk bot using python flask

## 이 프로젝트는 더 이상 유지보수 되지 않습니다.
**대신 [chatterbox](https://github.com/jungwinter/chatterbox)를 사용해주세요.**

## 1. 소개
[카카오톡 옐로아이디 자동응답 API Specification](https://github.com/plusfriend/auto_reply)을 충족시키는 파이썬 구현체입니다.  
옐로아이디 자동응답 서비스(e.g. 챗봇)를 파이썬으로 구현할 때 저장소를 포크한 후 코드를 수정하여 사용하시면 됩니다.  
Python 3, Flask 0.12, SQLAlchemy 1.1.4를 기준으로 구현되었으며 그 외의 의존성 패키지들은 `requirement.txt`에서 확인하실 수 있습니다.

### 상세
- `run.py` : 서비스를 실행시킵니다. uwsgi를 사용한다면 이 파일을 module로 지정시켜야 합니다.
- `app/`
  - `view.py` : Flask의 진입점이며 사용자의 요청을 라우팅합니다.
  - `config.py` : DB파일의 저장경로 및 여러 Flask설정을 관리합니다.
  - `manager.py` : 로직을 처리하는 handler들을 정의합니다.
    - `APIManager` : 분기에 따라 `MessageManager`를 호출하고 요청을 처리합니다.
    - `MessageManager` : Message객체를 생성시키고 message를 `APIManager`에 제공합니다.
    - `DBManager` : DB를 관리합니다.
  - `message.py` : 여러 기본 메시지 타입이 선언되어 있습니다.
  - `keyboard.py` : 메시지에 포함되는 키보드를 정의합니다.
  - `model.py` : DB모델들을 정의합니다.

## 2. 사용방법

### 1. 옐로아이디 생성
[카카오톡 옐로아이디 자동응답 API Specification](https://github.com/plusfriend/auto_reply) 의 `3. 이용 시작하기` 항목을 참고해 옐로아이디의 자동응답 서비스를 개시합니다.

### 2. Yellowid-Flask 저장소 Fork
우측 상단의 Fork버튼을 눌러 자신의 Github계정에 Yellowid-Flask 저장소를 생성합니다.

### 3. 저장소 Clone
```shell
$ cd ~
$ git clone git@github.com:<your id>/yellowid-flask.git
```
Github GUI 등 다른 방법으로도 Clone하실 수 있습니다.

### 3. 가상환경 설정
```shell
$ cd ~/yellowid-flask
$ virtualenv venv -p python3
$ source ./venv/bin/activate
```

### 4. 의존성패키지 설치
```shell
(venv) $ pip install -r requirement.txt
```

### 5. 실행
```shell
(venv) $ cd ~/yellowid-flask
(venv) $ python run.py
```
실행하면 `app/model.py` 에 정의된 DB테이블이 자동으로 생성됩니다.  
기본으로 생성되는 위치는 `yellowid-flask/app/`이며 `dbname.db`로 생성됩니다.  
이 후 [옐로아이디 자동응답 API 페이지](https://yellowid.kakao.com/bot/api)에서 앱 URL을 `http://server_ip:5000` 로 설정하고 `API TEST`을 통해 정상적으로 작동하는지 확인할 수 있습니다.

## 3. 배포
원하는 서비스에 맞게 yellowid-flask를 구현하고 배포하기 위해서 여러 방법을 사용하실 수 있습니다.  
`apache2`, `nginx`웹서버와 `uwsgi`를 조합해 배포할 수 있으며, `Tornado`, `Gunicorn`등 의 독립 wsgi 컨테이너를 사용할 수도 있고, `Heroku`, `Google App Engine`, `AWS`등의 플랫폼을 사용하실 수도 있습니다.

## 4. 활용 예
- [홍익대학교 학식알리미](https://github.com/JungWinter/HongikFood)
