---
title: "Flask에서 Pyrebase4로 Firebase Realtime Database 연결하기"
date: 2026-11-24
---

## 1. 프로젝트 배경

이음방 프로젝트에서는 회원 정보, 방 정보, 후기 등의 데이터를 저장하기 위해 Firebase Realtime Database를 사용한다. Flask 애플리케이션에서 Firebase에 접근하기 위해 Python 라이브러리인 `Pyrebase4`를 사용하였다.

이 글에서는 Flask 프로젝트에서 Pyrebase4를 설치하고, Firebase Realtime Database와 연결하기 위한 기본 설정 과정을 단계별로 설명한다.

## 2. Pyrebase4 설치하기

먼저 터미널에서 프로젝트 폴더로 이동한 뒤 Pyrebase4를 설치한다.

```bash
pip install pyrebase4
```

이음방 프로젝트의 `requirements.txt` 파일에는 Flask와 Pyrebase4가 등록되어 있기 때문에 다음 명령어를 사용하면 프로젝트에 필요한 라이브러리를 한 번에 설치할 수도 있다.

```bash
pip install -r requirements.txt
```

현재 프로젝트에서는 다음과 같이 필요한 패키지를 관리한다.

```text
Flask>=3.0,<4.0
pyrebase4
```

설치가 완료된 후 다음 명령어를 사용하여 Pyrebase4가 정상적으로 설치되었는지 확인할 수 있다.

```bash
pip show pyrebase4 | grep -E '^(Name|Version|Summary):'
```

패키지 이름과 버전 정보가 정상적으로 출력되면 Pyrebase4 설치가 완료된 것이다.

> 이 단계의 목적은 아직 Firebase와 직접 연결하는 것이 아니라, Flask 프로젝트에서 Firebase를 사용할 수 있도록 필요한 Python 라이브러리를 준비하는 것이다.

위 명령어를 실행한 결과 Pyrebase4의 이름과 버전 정보가 정상적으로 출력되었으며, 이를 통해 라이브러리가 정상적으로 설치된 것을 확인할 수 있다.

<img src="https://raw.githubusercontent.com/inoyashii/skills-github-pages/main/assets/images/pyrebase-install.png"
     alt="Pyrebase4 설치 확인"
     width="700">

## 3. Firebase 프로젝트 설정하기

Pyrebase4 설치가 완료되면 Firebase 프로젝트를 준비해야 한다. 이음방 프로젝트에서는 데이터를 저장하기 위해 Firebase Realtime Database를 사용하였다.

먼저 Firebase Console에서 프로젝트를 생성하거나 기존 프로젝트를 선택한다. 그다음 Realtime Database를 생성하여 애플리케이션에서 데이터를 저장할 수 있도록 준비한다.

Flask 애플리케이션에서 Firebase에 연결하려면 Firebase 프로젝트의 설정 정보가 필요하다. 이음방 프로젝트에서는 해당 정보를 별도의 JSON 파일로 저장하였다.

프로젝트 구조는 다음과 같다.

```text
project/
├── app.py
├── database.py
└── authentication/
    └── firebase_auth.json
```

`firebase_auth.json` 파일에는 Firebase 프로젝트와 연결하기 위한 설정 정보가 저장된다. 실제 프로젝트에서는 보안을 위해 실제 설정 값을 공개하지 않고, 다음과 같이 예시 형태로 표현할 수 있다.

```json
{
  "apiKey": "YOUR_API_KEY",
  "authDomain": "YOUR_PROJECT.firebaseapp.com",
  "databaseURL": "https://YOUR_PROJECT.firebaseio.com",
  "projectId": "YOUR_PROJECT",
  "storageBucket": "YOUR_PROJECT.appspot.com"
}
```

이 설정 파일은 이후 `database.py`에서 읽어 Firebase와 연결할 때 사용한다.

> 실제 프로젝트에서 사용하는 Firebase 설정 정보는 공개 저장소나 블로그에 그대로 노출하지 않는 것이 좋다.

## 4. Flask와 Firebase 연결하기

Firebase 설정 파일을 준비한 후 `database.py`에서 해당 파일을 읽어 Firebase Realtime Database와 연결한다.

먼저 필요한 라이브러리를 불러온다.

```python
import json
import pyrebase
```

그다음 `DBhandler` 클래스의 생성자에서 `firebase_auth.json` 파일을 읽고 Firebase를 초기화한다.

```python
class DBhandler:
    def __init__(self):
        f = open("./authentication/firebase_auth.json")
        config = json.load(f)
        f.close()

        firebase = pyrebase.initialize_app(config)
        self.db = firebase.database()
```

`json.load()`는 JSON 파일에 저장된 Firebase 설정 정보를 Python에서 사용할 수 있도록 불러온다.

`pyrebase.initialize_app(config)`는 해당 설정 정보를 이용하여 Firebase 프로젝트와 연결한다.

마지막으로 `firebase.database()`를 통해 Firebase Realtime Database에 접근할 수 있는 객체를 생성하고 `self.db`에 저장한다.

이후 데이터 저장이나 조회가 필요한 경우 `self.db`를 사용하여 Firebase의 데이터를 읽거나 수정할 수 있다.

예를 들어 현재 프로젝트에서는 다음과 같이 Firebase의 데이터를 불러올 수 있다.

```python
items = self.db.child("item").get().val()
```

이 코드는 Firebase Realtime Database의 `item` 경로에 저장된 데이터를 가져온다.

현재 이음방 프로젝트의 백엔드는 개발 중이기 때문에 기존 데이터 구조를 새로운 방, 후기, 물려주기 기능에 맞게 수정할 예정이다. 하지만 Flask와 Firebase를 연결하는 기본 방식은 동일하게 사용할 수 있다.

## 5. 데이터 저장 테스트

작성 예정

## 6. 실행 결과

작성 예정

## 7. 배운 점

작성 예정

## 참고자료

작성 예정

...
