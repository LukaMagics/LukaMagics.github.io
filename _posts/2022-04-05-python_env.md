---
title: "[Python] 가상환경, package 관리, pip install과 conda install 차이"

categories:
  - python
tags:
  - [Python, venv, dev env]

toc: true
toc_sticky: true
 
date: 2022-04-05
last_modified_at: 2022-04-05
---

📌 **작성자 개발 환경** <br>
**OS** : Windows 10 <br>
**Language** : Python<br>
**Tool** : Visual Studio Code<br>
{: .notice--primary}

# 1. 가상환경 생성과 패키지 관리의 필요성

<br>
Python을 시작으로 프로그래밍을 처음 접하면 유튜브나 블로그에서 설명하는대로 Python을 위한 개발환경을 구축한다. Python만 설치할 수도 있고, Anaconda3를 설치하여 Python 및 자주 쓰이는 package를 설치할 수도 있다. 초기에는 별도의 설치가 필요없는 Python 내장 라이브러리만 사용하다가 시각화, 데이터 핸들링, 머신러닝 등의 작업을 위해 matplotlib, numpy, pandas, tensorflow, scikit learn 등 패키지를 설치 및 import하게 된다.<br>
그러나 __개인이 만든 package나 tensorflow를 설치하기 시작하면 package 버전에 따른 호환성, 의존성 문제에 직면한다.__
<br>

## 1.1. 의존성(Dependency) 문제

- 의존성은 특정 패키지를 이용하기 위해 요구되는 다른 패키지를 말한다.
- 예를 들어, tensorflow를 import하기 위해선 numpy가 필요하며, tensorflow의 버전마다 요구되는 numpy 버전도 다를 수 있다.
- 여러 package를 설치하다보면 package 버전의 의존성에 의해 충돌이 발생한다.
- conda prompt, cmd 등 CLI (Command Line interface)에서 설치할 때 설치 자체가 에러로 인해 불가할 수 있고, 다 작성해놓은 소스코드를 compile할 때 에러가 발생할 수 있다. 
- 예를 들어, 버전 업데이트로 함수의 output shape이 달라졌거나 패키지에 없는 메서드를 호출할 수 있는 것이다.
<br>

# 2. 가상환경
<br>

## 2.2 가상환경 생성

- 우리는 패키지 버전이 맞지 않아 발생하는 error를 피하기 위해 독립적인 가상환경(개발 환경)을 구축한다.<br>
- 패키지 버전의 충돌로 인해, 가상환경(별도의 개발환경)을 구축하는 일은 Python 외 어떤 프로그래밍 언어로 작업하든 필연적이다.<br>

> 내가 이해하는대로 가상환경을 가장 쉽게 설명하면, PC에 별도의 폴더를 만드는 일과 비슷하다.<br>
예를 들어, 우리는 학부수업을 들을 때 수업자료, 과제 등을 모아놓는 폴더를 만든다. 폴더에는 여러 개의 한글(hwp) 파일들이 들어있다.<br>
개발을 위한 가상환경도 마찬가지다. 프로젝트마다 별도의 폴더를 만들어 코드 소스파일(.py)을 저장해둔다.<br>
차이가 있다면, 학부수업 폴더의 .hwp 파일을 실행하려면 PC에 한글이 설치되어 있으면 PC전역에서 문제 없이 실행할 수 있다. 하지만, 개발을 위한 가상환경은 한글 프로그램의 버전을 달리하여 별도로 소프트웨어를 설치하는 것으로 비슷하다.<br>
**문제 없이 소스코드를 실행하기 위해서는 그에 맞는 버전의 "Python.exe (interpreter)"과 "Package"가 요구된다.**

Python에서는 주로 가상환경 관리를 위해 venv, virtualenv, conda, poetry 등을 개별적으로 또는 조합하여 이용한다.
- **venv** : Python 3.3부터 내장 모듈이 되어 별도 설치("pip install venv")없이 사용 가능 **(아래 virtualenv를 경량화한 모듈)**
- **virtualenv** : pip install, conda install로 설치해야 함
- **conda** : Anaconda3 설치 시 "conda create -n venv"와 같이 conda를 붙여 가상환경 생성 및 관리를 위한 command 사용.
- **poetry** : conda와 유사하지만 패키지 의존성 관리를 보다 자동화할 수 있음.<br>
<br>

## 가상환경 내 패키지 관리
test3