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
그러나 __개인이 만든 package나 tensorflow를 설치하기 시작하면 package 버전에 따른 상호간의 호환성, 의존성 문제에 직면한다.__
<br>

## 1.1. 의존성(Dependency) 문제

- 의존성은 특정 패키지를 이용하기 위해 요구되는 다른 패키지를 말한다.
- 예를 들어, tensorflow를 import하기 위해선 numpy가 필요하며, tensorflow의 버전마다 요구되는 numpy 버전도 다를 수 있다.
- 여러 package를 설치하다보면 package 버전의 의존성에 의해 충돌이 발생한다.
- conda prompt, cmd 등 CLI (Command Line interface)에서 설치할 때 설치 자체가 에러로 인해 불가할 수 있고, 다 작성해놓은 소스코드를 compile할 때 에러가 발생할 수 있다. 
- 예를 들어, 버전 업데이트로 함수의 output shape이 달라졌거나 패키지에 없는 메서드를 호출할 수 있는 것이다.
<br>
<br>

# 2. 가상환경
<br>

## 2.1 가상환경 생성

- 우리는 패키지 버전이 맞지 않아 발생하는 error를 피하기 위해 독립적인 가상환경(개발 환경)을 구축한다.<br>
- 패키지 버전의 충돌로 인해, 가상환경(별도의 개발환경)을 구축하는 일은 Python 외 어떤 프로그래밍 언어로 작업하든 필연적이다.<br>

> 내가 이해하는대로 가상환경을 가장 쉽게 설명하면, PC에 별도의 폴더를 만드는 일과 비슷하다.<br>
예를 들어, 우리는 학부수업을 들을 때 수업자료, 과제 등을 모아놓는 폴더를 만든다. 폴더에는 여러 개의 한글(hwp) 파일들이 들어있다.<br>
개발을 위한 가상환경도 마찬가지다. 프로젝트마다 별도의 폴더를 만들어 코드 소스파일(.py)을 저장해둔다.<br>
차이가 있다면, 학부수업 폴더의 .hwp 파일을 실행하려면 PC에 한글이 설치되어 있으면 PC전역에서 문제 없이 실행할 수 있다. 하지만, 개발을 위한 가상환경은 한글 프로그램의 버전을 달리하여 해당 프로젝트 폴더에 한번 더 설치해두는 것이라 비유할 수 있다.<br>
**문제 없이 소스코드를 실행하기 위해서는 그에 맞는 버전의 <u>Interpreter</u>가 요구된다.**
**Interpreter는 소스코드를 실행하는 환경으로 python, package 등의 버전을 포함한다.** 

Python에서는 주로 가상환경 관리를 위해 **venv, virtualenv, conda, poetry** 등을 개별적으로 또는 조합하여 이용한다.
- **venv** : Python 3.3부터 내장 모듈이 되어 별도 설치없이 사용 가능 **(아래 virtualenv를 경량화한 모듈)**
- **virtualenv** : pip install, conda install로 설치해야 함
- **conda** : Anaconda3 설치 시 ```conda create -n venv```와 같이 conda를 붙여 가상환경 생성 및 관리를 위한 command 사용.
- **poetry** : conda와 유사하지만 패키지 의존성 관리를 보다 자동화할 수 있음.<br>
<br>

## 2.2 Interpreter의 이해 및 관리

- Python 버전에 의해 코드 실행 가능여부가 좌우될 수 있다.
- VSCode 같은 편집기에서는 interpreter를 선택하여 소스코드를 컴파일할 환경을 선택한다.
- 가상환경 이름이 "venv"라면 프로젝트 디렉토리 안에 ".venv" 디렉토리에 이 환경이 모두 구비되어 있어야 한다.
- **"./.venv/Lib/site-packages"** 경로에 설치한 "패키지(numpy, pandas 등)"들이 있다. 
- **"./.venv/Scripts"** 경로에 "python.exe"가 있다. 이 "python.exe" 파일의 버전이 Interpreter가 사용하는 python 버전이다. 

- <span style="color:blue">Q. interpreter는 추가적으로 무엇이 있어야하고 어떻게 작동하는가?</span><br>
- <span style="color:blue">Q. wheel.exe 파일도 있는데, 이것은 어떤 기능을 수행하는가?</span><br>
- <span style="color:blue">Q. pip.exe도 있는데, 패키지들이 모여있는 site-package 에도 pip가 있다. pip는 conda처럼 command를 사용할 수 있는데 왜 패키지에도 있는가?</span><br>
<br>

### 2.2.1 Python 버전 관리

- 가상환경마다 필요한 버전의 python.exe가 설치되어 있어야 한다.
- Python 홈페이지에서 직접 다운받을 수 있지만 번거롭기 때문에 주로 **conda, pyenv**를 이용한다.
- **conda** 명령어를 이용해 CLI 환경에서 가상환경을 생성할 때 Python 버전을 미리 지정해 설치할 수 있다. 가상환경을 생성할 때 python 버전을 지정안했다면 PC 전역에서 default (global)에 해당하는 Python 버전이 설치된다.

**conda**는 venv와 달리 가상환경을 현재 폴더에 생성하지 않고 Anaconda 설치 폴더의 envs 안에 생성되기 때문에 디렉토리를 옮겨다닐 필요가 없다.
<br>

**conda: Python 버전 지정하여 가상환경 생성**<br>
```
> conda create -n [ENV_NAME] python=3.7
```
**conda: python 버전 변경**<br>
```
> conda install python=3.7
```

**pyenv**는 Python 버전을 관리해주는 툴이며, 별도로 설치가 필요하다. **pyenv**는 새로운 Python 버전이 필요하면 cmd 창에서 바로 다운받고, 버전을 왔다갔다 전환할 수 있다.
<br>

**pyenv 설치 (cmd 창)**
```
pip install pyenv-win --target %USERPROFILE%\.pyenv 
```
target 다음엔 설치 경로입력. 환경변수를 추가해줘야 되기 때문에 사용자 폴더 내 설치해주자.

<img src="./assets/images/pyenv_path.jpg" width="450px" height="300px" title="pyenv환경변수" alt="pyenv_path"></img><br/>

<br>

### 2.2.2 패키지 의존성 관리
<br>
pip 파이썬 2.7.9 이후 버전과 파이썬 3.4 이후 버전은 pip를 기본적으로 포함한다.
<br>