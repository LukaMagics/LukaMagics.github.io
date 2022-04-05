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
- 가상환경 이름이 "venv"라면 프로젝트 디렉토리 안에 ".venv" 디렉토리에 이 환경이 모두 구비되어 있어야 한다.(단, conda와 같이 한 폴더에 가상환경이 모여있는 경우는 해당하지 않는다)
- **"%나의프로젝트폴더%/.venv/Lib/site-packages"** 경로에 설치한 "패키지(numpy, pandas 등)"들이 있다. 
- **"%나의프로젝트폴더%/.venv/Scripts"** 경로에 "python.exe"가 있다. 이 "python.exe" 파일의 버전이 Interpreter가 사용하는 python 버전이다. 

- <span style="color:blue">Q. interpreter는 추가적으로 무엇이 있어야하고 어떻게 작동하는가?</span><br>
- <span style="color:blue">Q. wheel.exe 파일도 있는데, 이것은 어떤 기능을 수행하는가?</span><br>
- <span style="color:blue">Q. pip.exe도 있는데, 패키지들이 모여있는 site-package 에도 pip가 있다. pip는 conda처럼 command를 사용할 수 있는데 왜 패키지에도 있는가?</span><br>

가상환경을 Interpreter로 활용하기 위해선 가상환경의 Python 버전과 packcage 버전 관리가 무엇보다 중요하다.<br>
다음 챕터에서는 **"conda(+pip)"**와 **"pyenv+poetry"** 두 가지 방식에서 각각 가상환경을 생성하고 관리하는 방법을 다뤄보고자 한다.<br>
- **"conda(+pip)"**: conda로 가상환경 생성, package 설치 및 의존성 관리/ pip로 conda에서 설치 불가한 package 설치
- **"pyenv+poetry"**: pyenv로 Python 버전 관리 / poetry로 가상환경 생성, package 설치 및 의존성 관리
> 개인적으로 conda(+pip)보다는 **"pyenv+poetry"** 조합을 추천한다. conda+poetry 조합을 사용하기도 하는데 어떤 이점이 있는지는 잘 모르겠다.
<br>

### 2.2.1 conda(+pip) 가상환경 생성
<br>
가상환경에서는 소스코드 실행에 필요한 Python 버전(python.exe)이 설치되어 있어야 한다.<br>
Python 설치는 공식 홈페이지에서 직접 다운받을 수 있겠지만 번거롭기 때문에 주로 **conda나 pyenv**를 이용한다. (anaconda3 설치 시 Python 포함됨)<br>
참고로, pip 명령어는 Python 2.7.9 이후 버전 또는 3.4 이후 버전에서 Python 설치 시 기본적으로 포함된다.<br>
또한, conda 명령어는 anaconda3를 설치했으면 cmd나 conda prompt에서 사용할 수 있을 것이다.<br>

- **conda** 명령어를 이용해 cmd 창에서 가상환경을 생성할 때 Python 버전을 미리 지정해 설치할 수 있다.
- 가상환경을 생성할 때 python 버전을 지정안했다면 PC 전역에서 default (global)로 설정되어 있는 Python 버전으로 생성될 것이다.
- **conda**는 venv와 달리 가상환경을 현재의 폴더(cmd에서 현재 경로)에 생성하지 않고 Anaconda 설치 폴더의 envs 안에 생성되기 때문에 디렉토리를 옮겨다닐 필요가 없다.
<br>

**Python 버전을 지정하여 가상환경 생성(cmd 창에서 진행)**<br>
```
> conda create -n [ENV_NAME] python=3.7
```

**혹시나 기존 가상환경에 python 버전 변경(업/다운그레이드)하려면 아래 코드를 입력(py37 예시)**<br>
```
> conda install python=3.7
```

**conda create로 생성한 가상환경에 패키지를 설치하려면 아래 코드로 가상환경을 먼저 활성화시켜줘야 한다.**

```
> conda activate [ENV_NAME]
```

- 이제 패키지를 설치해보자
- Python의 package 설치 방식 중 가장 많이 사용하는 것이 pip install과 conda install일 것이다.
- (윈도우 OS 기준) cmd 창에서 다음 코드 중 하나를 실행하여 설치한다.

1.  ```pip install [PACKAGE_NAME]```
2.  ```conda install [PACKAGE_NAME]```

둘의 차이, pip3가 설치되는 경로와 위험성, conda 패키지 관리 팁

### 2.2.2 pyenv+poetry 가상환경 생성 (설치 포함)

<br>

<br>

**pyenv**는 Python 버전을 관리해주는 툴이며, 별도로 설치가 필요하다. pyenv는 새로운 Python 버전이 필요하면 cmd 창에서 바로 다운받고, 버전을 왔다갔다 전환할 수 있다.

**pyenv 설치 (cmd 창)**
```
pip install pyenv-win --target %USERPROFILE%\.pyenv 
```
target 다음엔 설치 경로입력. 환경변수를 추가해줘야 되기 때문에 사용자 폴더 내 설치해주자.<br>
그 다음엔 **"고급 시스템 설정 보기 - 고급 - 환경변수 - 시스템 변수(S) - 새로 만들기"**로 사진과 같이 아래 두 경로를 환경변수에 추가해준다.

<img src="/assets/images/pyenv_path.JPG" width="450px" height="300px">

**C:\users\%USERPROFILE%\.pyenv\pyenv-win\bin**
**C:\users\%USERPROFILE%\.pyenv\pyenv-win\shims**

이제 poetry로 가상환경을 생성할텐데, 그 전에 pyenv로 global Python 버전을 설정해줘야한다.

<br>