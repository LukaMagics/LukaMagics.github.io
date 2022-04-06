---
title: "[Python & Windows] pyenv, poetry, pip, conda, 가상환경, 패키지 관리 총 정리"

categories:
  - python
tags:
  - [Python, 파이썬, venv, 가상환경, pip, conda, poetry, pyenv]

toc: true
toc_sticky: true
 
date: 2022-04-05
last_modified_at: 2022-04-06
---

📌 **작성자 개발 환경** <br>
**OS** : Windows 10 <br>
**Language** : Python<br>
**Tool** : Visual Studio Code<br>
{: .notice--primary}

# 1. 가상환경 생성과 패키지 관리의 필요성

<br>
Python을 시작으로 프로그래밍을 처음 접하면 유튜브나 블로그에서 설명하는대로 Python을 위한 개발환경을 구축한다. Python만 설치할 수도 있고, Anaconda3를 설치하여 Python 및 자주 쓰이는 package를 설치할 수도 있다. 초기에는 별도의 설치가 필요없는 Python 내장 라이브러리만 사용하다가 시각화, 데이터 핸들링, 머신러닝 등의 작업을 위해 matplotlib, numpy, pandas, tensorflow, scikit learn 등 패키지를 설치 및 import하게 된다.<br>
그러나 __개인이 만든 package나 tensorflow를 설치하기 시작하면 package 버전에 따른 상호간의 호환성, 의존성 문제에 직면한다.__<br>
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
**Interpreter는 소스코드를 실행하려는 python 버전, package 버전 등을 나타낸다.** 

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


가상환경을 Interpreter로 활용하기 위해선 가상환경의 Python 버전과 packcage 버전 관리가 무엇보다 중요하다.<br>
다음 챕터에서는 **"conda(+pip)"**와 **"pyenv+poetry"** 두 가지 방식에서 각각 가상환경을 생성하고 관리하는 방법을 다뤄보고자 한다.<br>
- **"conda(+pip)"**: conda = 가상환경 생성, package 설치 및 의존성 관리 / pip = conda에서 설치 불가한 package 설치
- **"pyenv+poetry"**: pyenv = Python 버전 관리 / poetry = 가상환경 생성, package 설치 및 의존성 관리

> 개인적으로 conda(+pip)보다는 **"pyenv+poetry"** 조합을 추천한다. (conda+poetry 조합을 사용하기도 하는데 어떤 이점이 있는지는 잘 모르겠다)
**"pyenv+poetry"** 조합을 활용하면 익숙해지기 전까지 conda보다 활용은 어렵지만, 프로그래밍을 하다보면 내가 설치하고 싶은 package가 conda에 없어 불가피하게 pip install을 써야할 경우가 많다. pip install을 사용한다는 것은 결국 conda의 의존성 관리를 지원받지 못하게 된다. 그러나 **체감상 poetry를 사용하면 거의 대부분의 package를 설치할 수 있을 뿐만 아니라 의존성 관리도 할 수 있다.**

<br>

### 2.2.1 conda(+pip) 가상환경 생성하기
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
conda create -n [ENV_NAME] python=3.7
```

**혹시나 기존 가상환경에 python 버전 변경(업/다운그레이드)하려면 아래 코드를 입력(py37 예시)**<br>
```
conda install python=3.7
```

**conda create로 생성한 가상환경에 패키지를 설치하려면 아래 코드로 가상환경을 먼저 활성화시켜줘야 한다.**

```
conda activate [ENV_NAME]
```

- 이제 패키지를 설치해보자
- Python의 package 설치 방식 중 가장 많이 사용하는 것이 pip install과 conda install일 것이다.
- cmd 창에서 다음 코드 중 하나를 실행하여 원하는 package를 설치한다.

1.  ```pip install [PACKAGE_NAME]```
2.  ```conda install [PACKAGE_NAME]```

pip install과 conda install은 많이 다르기 때문에 주의해서 사용해야 한다.<br>
아래는 둘의 특징과 차이를 정리하였다.

<br>

#### 2.2.1.1 pip와 conda의 특징 및 차이점
- pip는 Python의 package만을 관리할 수 있지만, conda는 Python, java, C 등 conda가 관리하는 package라면 개발언어에 상관없이 관리할 수 있다(language-agnostic).
- package 의존성 관리 측면에서 conda가 훨씬 낫다. 설치하려는 package가 Python뿐만 아니라 다른 language를 포함하고 있다면 pip에서 에러가 발생할 수 있다.
- 특히, C 언어가 포함된 소스코드나 Mac OS(또는 Linux) 환경에서 만들어진 코드를 Windows OS에서 설치하고 Import할 때 에러가 자주 발생한다.
- pip는 Pypi서버에서 최신 패키지가 바로 업로드되기 때문에 pip install로 거의 모든 package를 설치할 수 있다. 
- 그러나 conda는 의존성을 검증하여 Anaconda repository & Anaconda Cloud에 업로드된 package를 지원하기 떄문에 개인이 만든 또는 마이너한 package는 conda install로 설치하지 못할 수 있다.
- Anaconda가 설치되어 있고(Python이 Anaconda에 포함되어 설치됐고 별도로 Python을 설치안했을 경우), 가상환경을 activate했을 때 pip와 conda install의 패키지 설치 경로는 동일하다.
  - 참고: Anaconda 설치 시 "all users" 선택했을 때 기준으로 "C:/ProgramData/Anaconda3" 경로 ("Just me"를 선택했다면 "C:/Users/%USER_NAME%/Anaconda3")
  - (가상환경O) **pip install**: C:/ProgramData/Anaconda3/envs/%ENV_NAME%/lib/site-packages
  - (가상환경O) **conda install**: C:/ProgramData/Anaconda3/envs/%ENV_NAME%/lib/site-packages
  - **pip install**: C:/ProgramData/Anaconda3/lib/site-packages
  - **conda install**: C:/ProgramData/Anaconda3/lib/site-packages<br>

> 단, conda 안에 있는 pip로 package를 설치하지 않고 Python을 별도로 설치했을 떄 생긴 pip로 설치할 경우 경로는 다를 것이다. <br>
또한 pip3 install ~ 을 할 경우 PC에 설치된 Python (3.0 version 이상) 경로에 설치되니 pip3는 사용하지 않아야 한다.
 
package 의존성 관리를 잘하기 위해선 pip와 conda install의 차이를 알고 있어야 하며,<br>
몇가지 규칙에 따라 사용할 필요가 있다.<br>
<br>

#### 2.2.1.2 conda(+pip) install 이용 시 규칙<br>

(**출처: [daewonyoon님](https://daewonyoon.tistory.com/311)**)

1. ```conda install [PACKAGE_NAME]``` 으로 conda를 통해 설치할 수 있는지 확인
2. ```conda install -c conda-forge [PACKAGE_NAME]```으로 설치. 1번은 conda의 default 채널에서 패키지를 내려받는 것으로 해당 채널에 패키지가 없으면 conda-forge 채널에서 찾아보는 것. daualt보다 최신의 package를 찾을 확률이 있으나 요새는 별로 차이가 없다고 한다.
3. 검색창에 "anaconda + 패키지명"으로 검색, anaconda.org 사이트 페이지가 있고, 해당 페이지에서 소개하는 채널을 이용하여 설치. ```conda install -c [CHANNEL] [PACKAGE_NAME]``` 명령으로 설치한다.
위 모든 것이 실패하였을 때에, pip install 한다.
4. pip install 시 의존성에 의해 설치된 패키지들 중에 conda install 이 가능한 패키지가 있다면, pip uninstall 한 후에 conda install 로 다시 설치.
5. 기본 환경인 **(base)**는 작업용으로 쓰지말고, ```conda create - n [ENV_NAME] python=[PYTHON_VERSION]```로 새 가상환경을 만들어 사용한다. 패키지끼리 충돌이 발생하였을 때에 테스트도 용이하고, 특정 패키지의 버전차이 테스트도 가능하고, 불가피하게 충돌되는 두가지 환경을 분리하여 작업환경을 설치할 수 있다.
6. 추가적으로 package 버전 수정(update)이 필요하다면, pip를 사용한 다음에 다시 conda 를 사용하는 것보다 새 가상환경을 만들어 설치하는 것이 최선이다.<br>
<br>


### 2.2.2 pyenv+poetry 가상환경 생성하기
<br>
Windows 환경에서 **pyenv**과 **poetry**의 설치부터 가상환경 생성하는 방법을 정리하였다.<br>
<u>현재 Anaconda를 설치하지 않았거나 삭제한 상태를 가정하고 진행한다.</u> 

<br>

#### 2.2.2.1 pyenv 설치 및 활용<br>

**pyenv**는 Python 버전을 관리해주는 툴이며, 별도로 설치가 필요하다. pyenv는 새로운 Python 버전이 필요하면 cmd 창에서 바로 다운받고, 버전을 왔다갔다 전환할 수 있다.

**pyenv 설치 (cmd 창)**
```
pip install pyenv-win --target %USERPROFILE%\.pyenv 
```
target 다음엔 설치 경로입력. 환경변수를 추가해줘야 되기 때문에 사용자 폴더 내 설치해주자.<br>
그 다음엔 **"고급 시스템 설정 보기 - 고급 - 환경변수 - 시스템 변수(S) - 새로 만들기"**로 사진과 같이 아래 두 경로를 환경변수에 추가해준다.

<img src="/assets/images/pyenv_path.JPG" width="450px" height="300px">

**C:\users\%USERPROFILE%\.pyenv\pyenv-win\bin** <br>
**C:\users\%USERPROFILE%\.pyenv\pyenv-win\shims**

이제 poetry로 가상환경을 생성할텐데, 그 전에 pyenv로 global(default)로 사용할 Python 버전을 설정해줘야한다.

**cmd 창에서 설치 가능한 Python 버전을 확인.**
```
> pyenv install --list
:: [Info] ::  Mirror: https://www.python.org/ftp/python
2.4-win32
2.4.1-win32
2.4.2-win32
2.4.3c1-win32
2.4.3-win32
2.4.4-win32
2.5-win32
...

```

**원하는 버전의 Python 설치**

```
pyenv install [PYTHON_VERSION] # [PYTHON_VERSION] 예시 = 3.8.0 
```

**설치된(사용 가능한) Python 버전 확인(예시)**

```
> pyenv versions
* 3.7.8 (set by C:\Users\%USER_NAME%\.pyenv\pyenv-win\version) # 현재 기본으로 설정된 버전
  3.8.0
```


**원하는 Python 버전을 PC의 기본 값으로 선택**

```
pyenv global [PYTHON_VERSION] # 작성자는 3.8.0 으로 입력
```

**현재 사용 중인 파이썬 버전만 확인할 때(versions -> version)**

```
> pyenv version
3.8.0 (set by C:\Users\%USER_NAME%\.pyenv\pyenv-win\version)
```
<br>

#### 2.2.2.2 poetry 설치 및 활용<br>

이제 가상환경 및 패키지 관리를 할 수 있는 **poetry**를 설치한다.

**poetry**는 cmd가 아닌 **window shell**을 켜서 아래 코드를 입력해준다.

```
(Invoke-WebRequest -Uri https://install.python-poetry.org -UseBasicParsing).Content | python -
```

혹시나 뭔가 잘못되어 **삭제하려면 위에서 --uninstall만 추가**하면 된다.

```Invoke-WebRequest -Uri https://install.python-poetry.org -UseBasicParsing).Content | python - --uninstall```

(참고: poetry가 윈도우에서 설치되는 경로는 "%USERPROFILE%\.poetry\bin")

**이제 다시 cmd로 돌아와서** 가상환경(프로젝트 폴더)을 만드려면 경로로 이동(```cd [PATH]```)한다.

**가상환경(프로젝트 폴더) 생성**

```
poetry new [PROJECT_NAME]  # 작성자의 [PROJECT_NAME] = poetry_test
```

경로에 프로젝트 폴더가 생성되었을 것이다.<br>
생성된 폴더를 확인해보자. ```cd [PROJECT_NAME]```으로 해당 디렉토리로 이동하여 폴더 구조를 출력해주는 ```tree /f``` 입력.

```
> tree /f
Folder PATH listing
Volume serial number is AC3F-74F4
C:.
│   pyproject.toml
│   README.rst
│
├───poetry_test
│       __init__.py
│
└───tests
        test_poetry_test.py
        __init__.py
```

여러 init 파일과 몇몇 폴더가 생겼는데 필요하면 쓰면 된다. 중요한 **pyproject.toml** 파일은 남겨둔다.<br>
이제 설치할 package를 ```poetry add``` 명령어로 설치해줄 것이다. <br>
```poetry add```로 package를 추가하면 설치할 패키지의 의존성(Dependency)에 맞게 설치와 업데이트, 제거해야할 패키지의 정보를 검사 및 기록하고 package를 설치해준다. <br>
이에 대한 모든 정보는 **pyproject.toml**과 add 후에 생기는 **poetry.lock** 파일에 기록되며, <u>pyproject.toml가 requirement.txt, setup.py 역할을 한다고 보면 된다.</u>

**현재 cmd 내 경로가 프로젝트 폴더인지 한번 더 확인하고, 원하는 package를 add해준다** <br>
**(작성자는 예시를 위해 pandas==1.2.0을 add)**

```
> poetry add "pandas == 1.2.0"  # 특정 버전 이상 설치 시 "pandas >= 1.2.0" 가능

Updating dependencies
Resolving dependencies...

Writing lock file

Package operations: 15 installs, 0 updates, 0 removals

  • Installing pyparsing (3.0.7)
  • Installing six (1.16.0)
  • Installing atomicwrites (1.4.0)
  • Installing attrs (21.4.0)
  • Installing colorama (0.4.4)
  • Installing more-itertools (8.12.0)
  • Installing numpy (1.22.3)
  • Installing packaging (21.3)
  • Installing pluggy (0.13.1)
  • Installing py (1.11.0)
  • Installing python-dateutil (2.8.2)
  • Installing pytz (2022.1)
  • Installing wcwidth (0.2.5)
  • Installing pandas (1.2.0)
  • Installing pytest (5.4.3)
```

위와 같이 pandas==1.2.0을 설치하기 위해 필요한 설치, 수정, 제거 package 목록이 나타난다. (설치해야할 package가 15개로 나타났다.)

이제 프로젝트 폴더를 확인해보면 구체적인 package, version, dependency가 기록된 **poetry.lock** 파일과 가상환경 **.venv**이 생겨났을 것이다.<br>
**pyproject.toml** 및 **poetry.lock** 파일을 열어보면 모든 의존성 정보들이 기록된 것을 확인할 수 있다.<br>
또한 **.venv/Lib** 안에 package가 설치되었고, **.venv/Scripts** 안에 (자신이 설정한 version의) **python.exe** 가 설치되었을 것이다.<br>
<br>

#### 2.2.2.3 VSCode Interpreter로 설정하기<br>

VSCode 편집기에서 지금까지 생성한 poetry 가상환경을 Interpreter로 사용하려면 아래 과정을 거치면 된다.

1. VSCode에서 **프로젝트 폴더를 open** 해준다. ("File" > "Open file")
2. **Interpreter**를 해당 가상환경으로 설정하기 위해 **Ctrl+Shift+p > "Python: Select Interpreter" 검색 및 클릭 > "Enter interpreter path" 클릭 > "Find..." 클릭** 후 아래 사진처럼 **"/.venv/Scripts/python.exe"**를 선택.

<center><img src="/assets/images/poetry_vscode_interpreter2.png" width="1007px" height="684px"></center>

3. VSCode를 껐다가 다시 켜준다.
4. **Ctrl+Shift+p > "Python: Select Interpreter" 클릭 > "★ Python 3.8.0 ('.venv': poetry)"** 이런 형태로 되어있으면 Interpreter가 잘 선택된 것이다.

----

끝으로, **pyproject.toml** 파일을 통해 다른 PC에서 같은 가상환경을 쉽게 설치할 수 있다. 또한 **poetry.lock** 파일까지 있다면 완전히 일치하는 버전으로 가상환경을 세팅할 수 있다. <br>
간단히 설명하면, 가상환경을 구성할 폴더에 **pyproject.toml** 및 **poetry.lock**를 넣어주고 cmd 창에서 해당 디렉토리 경로로 이동해 ```poetry install``` 만 입력하면 된다.<br>
```poetry install```은 폴더 내 **pyproject.toml** 및 **poetry.lock** 파일을 인식하여 설치해준다.

> 다양한 poetry 명령어는 [python-poetry document](https://python-poetry.org/docs/cli/)에서 확인할 수 있다.
<br>