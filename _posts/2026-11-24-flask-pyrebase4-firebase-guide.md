---
title: "Flask에서 Pyrebase4로 Firebase Realtime Database 연결하기"
date: 2026-11-24
---
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

![Pyrebase4 설치 확인](/skills-github-pages/assets/images/pyrebase-install.png)

## 3. Firebase 프로젝트 설정하기

작성 예정

## 4. Flask와 Firebase 연결하기

작성 예정

## 5. 데이터 저장 테스트

작성 예정

## 6. 실행 결과

작성 예정

## 7. 배운 점

작성 예정

## 참고자료

작성 예정

...
