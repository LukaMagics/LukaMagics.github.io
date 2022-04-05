---
title: "[Python] pip install과 conda install 차이 정리: 개발환경(가상환경) 구축 관점"

categories:
  - python
tags:
  - [Python, venv, dev env]

toc: true
toc_sticky: true
 
date: 2022-04-05
last_modified_at: 2022-04-05
---

본 게시글에서는 개발환경 또는 가상환경을 구축할 때 발생할 수 있는 문제를 이해하기 위해 pip install과 conda install의 차이를 정리한다.

# 1. 깔끔한 개발환경에 대한 욕구
 
 처음 프로그래밍을 배우는 사람들이 Python을 이용하고자 한다.
 그들은 유튜브나 블로그 게시글에서 설명하는대로 Python을 이용할 수 있는 개발환경을 구축할 것이다.
 검색 창에 Python 3를 검색해서 Python만 설치할 수도 있고, 강의 영상에서 추천한대로 Anaconda3를 설치할 수도 것이다.

 초기에는 별도의 설치가 필요없는 Python 내장 라이브러리만으로 충분할 것이며, 데이터 시각화, 핸들링, 머신러닝 등의 작업을 위해 점차 matplotlib, numpy, pandas, tensorflow, scikit learn 등 유명한 패키지들을 설치하고 import하여 사용하게 된다.
 
 ## 1.1. 의존성 문제
 잘 사용하고 있었으나, tensorflow 또는 사람들이 만든 패키지를 설치할 때부터 애를 먹게 된다. conda prompt, cmd 등 CLI (Command Line interface)에서 잘 설치되던 패키지들이 점차 충돌하기 시작한다(의존성 문제).
 Jupyter Notebook의 !pip install 명령어도 마찬가지다. 
 
 여기서, 패키지의 의존성(Dependency)은 특정 패키지를 이용하기 위해 요구되는 다른 패키지를 말한다. 
 예를 들어, tensorflow를 import하기 위해선 numpy가 필요하다. 
 tensorflow의 버전마다 요구되는 numpy 버전도 다르다.
 기존에 내 PC에 설치되어 있던 특정 버전의 numpy가 지금 설치하는 tensorflow에 호환되지 않을 수 있다. 
 **다른 사람의 코드를 사용해보려는데 패키지 설치하는 데 1시간, 2시간 삽질하다보면 사람이 미친다.**

 ## 1.2. 가상환경 구축과 패키지 관리의 시작
 우리는 패키지 설치 과정에서 발생하는 error가 짜증나서 점차 패키지를 관리하고 가상환경을 구축한다.
 기존에 무턱대고 로컬 PC에 설치한 지저분한 패키지들이 보기 싫어졌다.
 새로운 마음으로 새로운 곳에서 코드를 실행하고 싶어진다. 이 때 우리는 독립적인 관리할 수 있는 가상환경을 만든다.

 패키지 버전의 충돌로 인해, 가상환경(별도의 개발환경)을 구축하는 일은 Python 외 어떤 프로그래밍 언어로 작업하든 필연적이다.
 내가 이해하는대로 가상환경을 가장 쉽게 설명하면, PC에 별도의 폴더를 만드는 일과 비슷하다.
 예를 들어, 우리는 학부수업을 들을 때 수업자료, 과제 등을 모아놓는 폴더를 만든다. 폴더에는 한글(hwp), 파워포인트(ppt) 파일들이 들어있다.
 개발을 위한 가상환경도 마찬가지다. 프로젝트마다 별도의 폴더를 만들어 코드 소스파일(.py)을 저장해둔다.
 차이가 있다면, 학부수업 폴더의 hwp, ppt 파일을 실행하려면 PC에 한글과 파워포인트가 깔려있으면 되지만, 개발을 위한 가상환경은 hwp, ppy 파일을 실행하기 위해 별도로 한글과 파워포인트 프로그램을 설치하는 것으로 비슷하다고 설명할 수 있다.
 **특정 코드를 실행하기 위해서는 그에 맞는 Python 버전(interpreter)과 Package 버전이 요구된다.**

 Python에서는 주로 가상환경 관리를 위해 venv, virtualenv, conda 등을 이용한다.
 - venv: Python 3.3(3.4?)부터 기본 모듈이 된 가상환경 관리 모듈. 기본 모듈이라 별도 설치("pip install venv")없다. 
 - venv나 virtualenv (이를 경량화한 모듈이 venv라고 한다) 모듈, conda 툴을 통해 , 

 패키지 관리 툴은 pip install을 통해 Python의 PyPI 파이썬 
 우리는 conda, pip와 같은 패키지 관리 툴을 통해 패키지를 설치한다. 

 Google Colab과 같이 Local (본인 PC) 환경이 아닌 경우엔 문제가 적을 수 있다. (Colab이



 

## test2
test3